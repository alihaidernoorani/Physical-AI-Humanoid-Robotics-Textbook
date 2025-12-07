---
id: 1
title: Create Textbook Constitution
stage: constitution
date: 2025-12-07
surface: agent
model: claude-sonnet-4-5-20250929
feature: none
branch: master
user: user
command: /sp.constitution
labels: [constitution,physical-ai,robotics,textbook]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
 - .specify/memory/constitution.md
tests:
 - none
---

## Prompt

```text
Project: Physical AI & Humanoid Robotics Textbook

1. Mission & Purpose

Create an academically rigorous, technically accurate, and highly structured textbook that introduces, explains, and expands the field of Physical AI, Embodied Intelligence, and Humanoid Robotics, grounded in verifiable, state-of-the-art research.
The constitution governs all content generation, review, editing, and verification across the full book creation process.

2. Core Principles

Scientific Accuracy

Every factual claim must be traceable to a verifiable source.

Prefer primary research from robotics, embodied cognition, biomechanics, and AI/ML.

Academic Clarity

Write for an audience with an undergraduate-level background in computer science, robotics, or AI.

Define advanced terminology before use.

Reproducibility & Transparency

All methods, algorithms, mathematical formulations, and conceptual frameworks must be presented with enough detail to be reproducible.

Each chapter must clearly state assumptions, models, and dependencies.

Rigor & Peer-Review Standards

Minimum 50% peer-reviewed sources from robotics/AI conferences and journals.

Prioritize sources such as: IEEE, Nature Robotics, Science Robotics, ACM, arXiv (with caution), RSS, ICRA, IROS.

Ethical & Safety Awareness

Consider ethical implications, safety constraints, societal impact, and human-robot interaction standards.

No unverified claims about capabilities or dangers.

3. Content Standards

Writing Grade Level: Flesch–Kincaid Grade 10–12

Tone: instructional, analytical, research-driven

Definition Requirements: Every chapter must include key term definitions

Visuals & Diagrams:

Non-copyright diagrams preferred

Provide descriptions of all figures for accessibility

4. Citation & Verification

Citation Format: APA 7th edition

Verification Rule:

No claim should appear unless verified by at least one reputable source.

Plagiarism Tolerance: 0% (all text must be original)

Source Types:

≥ 50% peer-reviewed academic sources

Remaining sources may include technical standards, robotics lab documentation, textbooks, reputable industry whitepapers, and specifications from leading robotics groups

5. Structural Requirements

Book Format: Docusaurus-based

Deployment: GitHub Pages

Minimum Length: 20–30 full chapters

Per-Chapter Requirements:

Learning objectives

Key definitions

Examples & illustrations

Summary

Citations section

Glossary entries where needed

6. Constraints

Total Word Count: 30,000–50000 words

Minimum Sources: 40+

Mathematical Accuracy:

Use canonical equations from robotics, control theory, machine learning, and embodied intelligence

Include symbolic definitions for all variables

No hallucinated references under any circumstances.

7. Success Criteria

The book is considered complete only if:

All factual claims are source-verified

Plagiarism check shows 0%

All references are real, valid, and publicly verifiable

Content passes an academic-level fact-checking review

Book builds a coherent narrative from Physical AI foundations → humanoid robotics systems → future directions

Final Docusaurus version builds and deploys successfully on GitHub Pages

8. Workflow Requirements (Spec-Kit Plus Compatible)

Use Spec-Kit Plus to create:

/sp.chapter

/sp.glossary

/sp.diagram.description

/sp.proto

/sp.checklist

Each chapter must be generated through a spec-first workflow: outline → draft → verify → revise.
```

## Response snapshot

Created a comprehensive constitution for the Physical AI & Humanoid Robotics Textbook project based on the user's requirements. The constitution includes:

- Core Principles: Scientific Accuracy, Academic Clarity, Reproducibility & Transparency, Rigor & Peer-Review Standards, Ethical & Safety Awareness, and Content Verification & Plagiarism Standards
- Structural Requirements: Book Format & Deployment standards and Visual & Accessibility standards
- Development Workflow: Chapter Creation Process and Content Constraints
- Governance: Rules for compliance and amendment procedures

The constitution file is now stored at .specify/memory/constitution.md with version 1.0.0.

## Outcome

- ✅ Impact: Created foundational constitution document for Physical AI textbook project
- 🧪 Tests: none
- 📁 Files: Updated .specify/memory/constitution.md
- 🔁 Next prompts: Chapter creation using /sp.chapter, glossary generation using /sp.glossary
- 🧠 Reflection: The constitution establishes clear academic and technical standards for the textbook project

## Evaluation notes (flywheel)

- Failure modes observed: none
- Graders run and results (PASS/FAIL): PASS
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): Begin creating first chapter using /sp.chapter