---
id: ros2-topics-services-actions
title: "Advanced ROS 2 Communication Patterns"
description: "Deep dive into Quality of Service, complex services, and action patterns in ROS 2"
personalization: true
translation: ur
learning_outcomes:
  - "Configure and optimize Quality of Service (QoS) policies for different robot communication needs"
  - "Implement complex service interfaces for synchronous robot operations with error handling"
  - "Design and implement action-based interfaces for long-running robot behaviors with feedback"
  - "Analyze and optimize communication performance for real-time humanoid robot systems"
software_stack:
  - "ROS 2 Humble Hawksbill (LTS)"
  - "Python 3.10+ with rclpy"
  - "RViz2 for visualization"
  - "Colcon for building packages"
hardware_recommendations:
  - "NVIDIA Jetson Orin Nano Development Kit"
  - "Intel RealSense D455 Depth Camera"
  - "ROS-compatible humanoid robot platform (e.g., ROSbot 2 PRO, TIAGo)"
hardware_alternatives:
  - "Raspberry Pi 4 with camera module (budget option)"
  - "Laptop with ROS 2 simulation environment"
prerequisites:
  - "Module 1 intro: Understanding ROS 2 as the robotic nervous system"
  - "ROS 2 Nodes chapter: Basic node architecture and communication patterns"
  - "Python programming fundamentals"
  - "Basic understanding of robotics concepts"
assessment_recommendations:
  - "Practical exercise: Configure QoS policies for different communication scenarios"
  - "Quiz: Identify appropriate communication patterns for given robot behaviors"
dependencies: ["01-ros2-nervous-system/intro", "01-ros2-nervous-system/01-ros2-nodes"]
---

# Advanced ROS 2 Communication Patterns

## Learning Objectives

- Configure and optimize Quality of Service (QoS) policies for different robot communication needs
- Implement complex service interfaces for synchronous robot operations with error handling
- Design and implement action-based interfaces for long-running robot behaviors with feedback
- Analyze and optimize communication performance for real-time humanoid robot systems

## Quality of Service (QoS) in Depth

Quality of Service (QoS) policies in ROS 2 provide fine-grained control over communication characteristics, enabling precise tuning for different robot applications. For humanoid robots, where different subsystems have varying requirements for reliability, latency, and data delivery, QoS policies are essential for achieving optimal performance (Macenski, 2022).

The DDS-based architecture of ROS 2 implements QoS through a combination of policies that can be applied independently to publishers and subscribers. The primary QoS policies include reliability (best-effort vs. reliable), durability (volatile vs. transient-local), history (keep-all vs. keep-last), and deadline settings. For humanoid robots, IMU data critical for balance control requires reliable delivery and low latency, while camera feeds for perception might tolerate best-effort delivery with higher latency (DDS, 2015).

Reliability policies determine how messages are delivered between nodes. For safety-critical applications like humanoid balance control, reliable reliability ensures that all messages are delivered, though with potentially higher latency. Best-effort reliability provides lower latency but does not guarantee message delivery, making it suitable for sensor data where occasional message loss is acceptable. The choice between these policies directly impacts the robot's ability to maintain stable operation under varying network conditions (Rivera et al., 2020).

Durability policies control how messages are retained for late-joining subscribers. Transient-local durability ensures that newly connected subscribers receive the most recent messages, which is valuable for visualization tools or logging nodes that may connect after system startup. Volatile durability provides the highest performance by not retaining messages for late subscribers, making it appropriate for high-frequency sensor data where only the most current information is relevant (Faconti et al., 2019).

History policies determine how many messages are stored for delivery. Keep-all history stores all messages until they are delivered, which can consume significant memory but ensures no data loss. Keep-last history stores only the most recent messages, balancing memory usage with data availability. For humanoid robots, the choice of history policy depends on the criticality of the data and the available system resources (Shibata et al., 2021).

## Advanced Service Implementations

Complex service interfaces in ROS 2 extend basic request-response patterns to handle sophisticated robot operations with comprehensive error handling and state management. In humanoid robotics, services often manage operations that require guaranteed delivery and specific responses, such as calibration routines, configuration changes, or state queries with complex return values (Macenski, 2022).

Service implementations in ROS 2 support complex request and response message types that can include arrays, nested structures, and custom message definitions. For humanoid robots, this capability enables services that return comprehensive state information, perform complex calculations, or coordinate multiple subsystems. The synchronous nature of services ensures that clients receive definitive responses, which is critical for safety-related operations where the outcome must be known before proceeding (Rivera et al., 2020).

Error handling in service implementations follows ROS 2's exception and return code patterns, allowing servers to communicate specific failure modes to clients. For humanoid robots, this is particularly important for operations that could affect safety or system stability. Service servers should implement comprehensive error checking and provide meaningful error messages that enable clients to take appropriate recovery actions (Shibata et al., 2021).

Service timeouts and retry mechanisms are essential for robust robot operation. Clients should implement appropriate timeout values based on the expected service execution time, and include retry logic for non-critical operations that might fail due to temporary system conditions. For humanoid robots, timeout values must balance responsiveness with the time required for complex operations, particularly those involving physical movement or sensor data processing (Faconti et al., 2019).

## Action Server and Client Patterns

Action-based communication in ROS 2 provides sophisticated interfaces for long-running operations with feedback, goal preemption, and result delivery. For humanoid robots, actions are essential for complex behaviors such as navigation, manipulation, and coordinated motion sequences that require continuous monitoring and potential interruption (Macenski, 2022).

The action architecture includes three distinct communication channels: goal, feedback, and result. The goal channel allows clients to send detailed objectives to action servers, including parameters and constraints. The feedback channel provides continuous updates on the progress of the operation, enabling other systems to coordinate appropriately. The result channel delivers the final outcome of the operation, including any relevant data or status information (Rivera et al., 2020).

Action servers implement state machines that manage the lifecycle of long-running operations. The typical action server state flow includes idle, active, succeeded, aborted, and preempted states. For humanoid robots, this state management is critical for maintaining system stability and enabling safe operation. The server must handle goal acceptance, execution monitoring, feedback generation, and proper cleanup upon completion or cancellation (Shibata et al., 2021).

Action clients provide interfaces for monitoring and controlling long-running operations. They can send goals to action servers, monitor progress through feedback, and send cancel requests when necessary. For humanoid robots, action clients must implement appropriate timeout and error handling to ensure that operations do not block the system indefinitely. The ability to preempt actions is particularly important for safety-critical robots that may need to interrupt ongoing behaviors in response to emergency situations (Faconti et al., 2019).

## Communication Performance Optimization

Optimizing communication performance in ROS 2 systems requires careful consideration of QoS policies, message sizes, and network topology. For humanoid robots, where real-time performance is critical, communication optimization directly impacts the robot's ability to respond to environmental changes and execute complex behaviors reliably (Macenski, 2022).

Message size optimization involves balancing the amount of information transmitted with the frequency of communication. Large messages provide comprehensive information but consume bandwidth and increase latency, while small messages reduce overhead but may require multiple transmissions to convey complete information. For humanoid robots, this balance is particularly important for sensor data, where the trade-off between data completeness and update frequency affects the robot's situational awareness (DDS, 2015).

Network partitioning strategies can improve communication performance by organizing nodes into logical groups with optimized QoS settings. For humanoid robots, this might involve separating safety-critical communication paths from less critical data streams, ensuring that critical information receives priority and reliable delivery. The use of multiple DDS domains or partitions can further isolate communication paths and prevent interference between different subsystems (Rivera et al., 2020).

Monitoring and profiling tools are essential for identifying communication bottlenecks and optimizing performance. ROS 2 provides tools for analyzing message rates, latency, and resource usage, which can be used to identify areas for improvement. For humanoid robots, continuous monitoring of communication performance is important for maintaining system stability and identifying potential issues before they affect robot operation (Shibata et al., 2021).

## Forward References to Capstone Project

The advanced communication patterns covered in this chapter are essential for implementing the complete humanoid robot system in the capstone project. The QoS configuration skills you learn here will be crucial for achieving real-time performance in the final system, particularly for safety-critical communication paths. The service and action patterns will be essential for implementing complex humanoid behaviors such as navigation, manipulation, and coordinated motion control.

## Ethical & Safety Considerations

The design of advanced communication patterns in humanoid robots has important ethical and safety implications. The reliability of QoS configurations affects the consistency of robot behavior, which directly impacts safety in human environments. Service calls for critical operations must be designed with appropriate timeouts and error handling to prevent system hangs that could lead to unsafe robot behavior. Actions for robot behaviors must include proper preemption capabilities to allow for emergency stops or safety interventions, particularly important as humanoid robots operate in close proximity to humans (Vander Hoek et al., 2019).

## Key Takeaways

- Quality of Service (QoS) policies provide fine-grained control over communication characteristics for different robot applications
- Complex service interfaces enable sophisticated robot operations with comprehensive error handling and state management
- Action-based communication supports long-running operations with feedback, goal preemption, and result delivery
- Proper QoS configuration is critical for achieving real-time performance in humanoid robot systems
- Communication performance optimization requires balancing message size, frequency, and reliability requirements
- Safety-critical communication paths should be isolated and prioritized in humanoid robot systems

## References

DDS. (2015). *Data Distribution Service (DDS) for Real-Time Systems*. Object Management Group.

Faconti, N., Paluri, M., & Breyer, M. (2019). *ROS 2 Design: client library architecture*. IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS).

Macenski, S. (2022). *Real-time performance in ROS 2*. Journal of Software Engineering for Robotics, 13(1), 45-62.

Rivera, S. S., Leturc, I., Rodriguez-Araujo, J., & Bouchard, M. (2020). ROS and ROS 2 compared in a real-time and distributed system for industrial applications. IEEE International Conference on Industrial Technology (ICIT), 1134-1139.

Shibata, H., Saito, T., & Sato, M. (2021). Distributed robotic systems using ROS 2: Architecture and applications. Advanced Robotics, 35(8), 467-482.

Vander Hoek, K., Hart, S., Belpaeme, T., & Feil-Seifer, D. (2019). Socially assistive robotics: A focus on trust and trustworthiness. IEEE International Conference on Robotics and Automation (ICRA), 8374-8380.