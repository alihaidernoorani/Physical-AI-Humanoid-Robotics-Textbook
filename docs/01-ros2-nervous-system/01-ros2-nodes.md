---
id: ros2-nodes
title: "ROS 2 Nodes, Topics, Services, and Actions"
description: "Understanding the fundamental communication patterns in ROS 2"
personalization: true
translation: ur
learning_outcomes:
  - "Design and implement ROS 2 nodes for humanoid robot systems"
  - "Configure Quality of Service (QoS) policies for different communication patterns"
  - "Implement topic-based communication for sensor and actuator data streams"
  - "Create service-based interfaces for synchronous robot operations"
  - "Develop action-based interfaces for long-running robot behaviors"
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
  - "Python programming fundamentals"
  - "Basic understanding of robotics concepts"
assessment_recommendations:
  - "Practical exercise: Create a simple ROS 2 node"
  - "Quiz: Identify communication patterns in given scenarios"
dependencies: ["01-ros2-nervous-system/intro"]
---

# ROS 2 Nodes, Topics, Services, and Actions

## Learning Objectives

- Design and implement ROS 2 nodes for humanoid robot systems
- Configure Quality of Service (QoS) policies for different communication patterns
- Implement topic-based communication for sensor and actuator data streams
- Create service-based interfaces for synchronous robot operations
- Develop action-based interfaces for long-running robot behaviors

## Understanding ROS 2 Nodes

ROS 2 nodes represent the fundamental computational units that execute specific robot functionality. In humanoid robotics, nodes encapsulate various capabilities such as sensor processing, motion control, perception, planning, and decision-making. Each node operates as an independent process, providing fault isolation and enabling distributed computation across multiple processing units—a critical requirement for humanoid robots with complex sensorimotor systems (Macenski, 2022).

The node architecture in ROS 2 differs significantly from ROS 1, incorporating improved lifecycle management and better support for real-time systems. A ROS 2 node can be implemented in multiple languages (C++, Python, Rust, etc.) and communicates with other nodes through topics, services, and actions. This multi-language support is particularly valuable in humanoid robotics, where different subsystems may require specialized languages for performance or legacy reasons (Rivera et al., 2020).

In humanoid robots, nodes are often organized by functional domains. For example, sensor driver nodes handle raw data acquisition from IMUs, cameras, and joint encoders. Perception nodes process this raw data to extract meaningful information such as object locations or environment maps. Planning nodes generate motion trajectories, and control nodes execute these trajectories on the robot's actuators. This functional separation enables modular development and independent optimization of each subsystem (Shibata et al., 2021).

## Topic-Based Communication

Topics in ROS 2 implement a publish-subscribe communication pattern that is ideal for sensor data distribution and state broadcasting. In humanoid robotics, topics are commonly used for continuous data streams such as joint states, sensor readings, and robot poses. The asynchronous nature of topic communication allows for efficient data distribution where multiple consumers can access the same information stream without blocking the publisher (Faconti et al., 2019).

Quality of Service (QoS) policies are a critical feature of ROS 2 topics that allow fine-tuning of communication characteristics. For humanoid robots, different sensor data streams require different QoS settings. For example, IMU data critical for balance control requires reliable delivery and low latency, while camera feeds for perception might tolerate best-effort delivery with higher latency. QoS policies include reliability (best-effort vs. reliable), durability (volatile vs. transient-local), history (keep-all vs. keep-last), and rate settings that can be configured based on the specific requirements of each data stream (DDS, 2015).

The pub/sub pattern is particularly beneficial for humanoid robots because it naturally supports the broadcast nature of sensor data. A single joint state publisher can provide information to multiple subscribers including controllers, visualizers, and logging nodes. This reduces system complexity and eliminates the need for multiple direct connections between components (Macenski, 2022).

## Service-Based Communication

Services provide synchronous request-response communication patterns suitable for operations that require acknowledgment and result delivery. In humanoid robotics, services are commonly used for operations that have a clear beginning and end, such as calibration routines, configuration changes, or state queries. Unlike topics, services establish a direct connection between the client and server for each request, ensuring that the client receives a response to its specific request (Rivera et al., 2020).

Service-based communication is appropriate for operations that require guaranteed delivery and specific responses. For example, a humanoid robot might use a service to request a specific joint calibration sequence, where the service response indicates success or failure. The synchronous nature of services ensures that the requesting node receives a definitive response, which is important for safety-critical operations (Shibata et al., 2021).

However, services are not suitable for continuous data streams or operations that might take extended periods to complete. The blocking nature of service calls means that the client node waits for the response, which could cause system delays if the service takes too long to execute. For long-running operations, actions are more appropriate (Faconti et al., 2019).

## Action-Based Communication

Actions extend services to support long-running operations with feedback and goal preemption. In humanoid robotics, actions are essential for behaviors that take extended time to complete, such as navigation to a goal, manipulation tasks, or complex motion sequences. Actions provide three key communication channels: goal, feedback, and result, allowing clients to monitor progress and cancel operations if necessary (Macenski, 2022).

The action architecture is particularly valuable for humanoid robot behaviors because it provides a standardized interface for complex operations while allowing for interruption and recovery. For example, a walking action might provide continuous feedback about the robot's current step phase, allowing other systems to coordinate appropriately. If the robot detects a dangerous situation, it can preempt the walking action to execute an emergency behavior (Rivera et al., 2020).

Actions use a client-server model where the action server executes the long-running behavior and the action client monitors progress and can send cancel requests. This design provides the flexibility needed for humanoid robot operations, where behaviors may need to be interrupted or modified based on changing environmental conditions or higher-level planning decisions (Shibata et al., 2021).

## Implementation Patterns for Humanoid Robotics

In humanoid robotics, nodes are often organized using design patterns that promote modularity and maintainability. The component-based architecture allows nodes to be composed from smaller, reusable parts, which is particularly useful for humanoid robots that share similar functionality across different subsystems. For example, multiple sensor drivers might share common component patterns for data processing and validation (Faconti et al., 2019).

The lifecycle node pattern provides enhanced control over node initialization, configuration, and shutdown, which is important for humanoid robots that need to transition between different operational states. Lifecycle nodes can be configured, activated, and deactivated in a controlled manner, allowing for safer robot operation and more predictable behavior during startup and shutdown sequences (DDS, 2015).

## Forward References to Capstone Project

The communication patterns learned in this chapter form the foundation for implementing the complete humanoid robot system in the capstone project. The node architecture you learn here will be used to structure the perception, planning, and control systems. Understanding QoS policies will be crucial for achieving real-time performance in the final system, and the action-based patterns will be essential for implementing complex humanoid behaviors.

## Ethical & Safety Considerations

The design of communication patterns in humanoid robots has important ethical and safety implications. The reliability of topic communication affects the consistency of sensor data, which directly impacts robot decision-making and safety. Service calls for critical operations must be designed with appropriate timeouts and error handling to prevent system hangs. Actions for robot behaviors must include proper preemption capabilities to allow for emergency stops or safety interventions (Vander Hoek et al., 2019).

## Key Takeaways

- Nodes provide the fundamental computational units for robot functionality with improved lifecycle management over ROS 1
- Topics enable efficient publish-subscribe communication with configurable Quality of Service policies
- Services provide synchronous request-response communication for operations requiring acknowledgment
- Actions support long-running operations with feedback and preemption capabilities
- Proper selection of communication patterns is critical for humanoid robot performance and safety
- QoS policies allow fine-tuning of communication characteristics for specific robot requirements

## References

DDS. (2015). *Data Distribution Service (DDS) for Real-Time Systems*. Object Management Group.

Faconti, N., Paluri, M., & Breyer, M. (2019). *ROS 2 Design: client library architecture*. IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS).

Macenski, S. (2022). *Real-time performance in ROS 2*. Journal of Software Engineering for Robotics, 13(1), 45-62.

Rivera, S. S., Leturc, I., Rodriguez-Araujo, J., & Bouchard, M. (2020). ROS and ROS 2 compared in a real-time and distributed system for industrial applications. IEEE International Conference on Industrial Technology (ICIT), 1134-1139.

Shibata, H., Saito, T., & Sato, M. (2021). Distributed robotic systems using ROS 2: Architecture and applications. Advanced Robotics, 35(8), 467-482.

Vander Hoek, K., Hart, S., Belpaeme, T., & Feil-Seifer, D. (2019). Socially assistive robotics: A focus on trust and trustworthiness. IEEE International Conference on Robotics and Automation (ICRA), 8374-8380.