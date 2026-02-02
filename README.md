# PiELo: A Reactive Infrastructure for Swarm Programming

**Authors:** Lorenzo Manfredi Segato, Filippo Marcantoni, Emma Pollak

**Project Advisor:** Carlo Pinciroli

**Institution:** Worcester Polytechnic Institute (WPI)

**Major Qualifying Project (Fall 2024 - Spring 2025):** Published on WPI Digital: [https://digital.wpi.edu/concern/student_works/wd3761406?locale=en]

---

## 1. Project Overview

PiELo is a domain-specific language (DSL) and runtime platform designed to simplify the development of decentralized robot swarms. It addresses the complexity of coordination and environmental response by treating **reactivity** and **consensus** as first-class language features.

### Project Goals

* **Simplified Reactivity:** Enable robots to automatically respond to sensor updates and environmental changes without complex callback chains.

* **Native Consensus:** Provide built-in mechanisms for individual robots to reach collective agreements and compute problems together.

* **Resource Efficiency:** Create a minimalist, stack-based infrastructure capable of running on resource-constrained robotic hardware.

* **Seamless Extensibility:** Allow high-level scripts to interface directly with low-level C++ hardware drivers for sensors and actuators.

---

## 2. System Architecture

The PiELo infrastructure is divided into two primary components: a compiler and a custom Virtual Machine (VM).

### Virtual Machine (VM)

The VM acts as a stack-based interpreter that executes compact bytecode.

* **Reactive Engine:** Maintains a directed acyclic graph (DAG) of dependencies to propagate changes through variables and closures.

* **Memory Management:** Implements a **mark-and-sweep garbage collector** to handle the lifecycle of reactive expressions and closures.

* **Symbol Tables:** Manages variable scopes across global, local, and shared environments.


### Compiler

The compiler translates Lisp-inspired source code into VM bytecode through three stages:

1. **Tokenization:** Lexical analysis of parenthesized prefix notation.

2. **Parsing:** Generation of an Abstract Syntax Tree (AST).

3. **Code Generation:** Emission of VM instructions, including special handling for reactive assignments.

---

## 3. Core Features & Modalities

### (i) First-Class Reactive Variables

Assignments can be declared as reactive, creating a persistent dependency between variables.

* **Automatic Synchronization:** When a source variable (e.g., a sensor) changes, all dependent variables are instantly re-calculated.

* **Boilerplate Reduction:** Eliminates the need for manual event listeners or "check loops".


### (ii) Automatic Variable Distribution (Shared Variables)

PiELo provides a mechanism for swarm-wide state synchronization.

* **Message Broker:** Uses a central server (or designated robot) to broadcast updates across the network.

* **Consistency:** Each update includes a local timestamp to maintain order across the decentralized swarm.


### (iii) Map Variables & Collective Coordination

Specialized data structures facilitate complex swarm patterns.

* **Key-Value Stores:** Maps are keyed by Robot ID, allowing individuals to contribute data to a collective datastructure.

* **Barrier Synchronization:** Enables robots to wait for a specific condition (e.g., all robots arriving at a point) before proceeding.

---

## 4. Software Stack & Dependencies

* **Language Syntax:** Lisp-inspired (prefix notation).

* **Implementation Language:** C++ (for the VM and native function registration).

* **Communication:** UDP/TCP via a message broker system for shared variables.

* **Extensibility:** Native C/C++ function registration interface for hardware integration (motors, sensors).

---

## 5. Experimental Evaluation

The effectiveness of PiELo was validated by comparing it against the **Robot Operating System (ROS)** using a "Barrier Test". Consensus was first validated in **ARGoS3 simulation**, and **Khepera IV robot deployments** using a Vicon motion-capture system..

* **PiELo Results:** Required significantly less code and overhead by leveraging native reactive primitives.

* **ROS Comparison:** ROS implementation required manual node management, custom message definitions, and extensive boilerplate for the same consensus logic.

---

## 6. Future Work

* **Decentralized Communication:** Transitioning from a central server model to a peer-to-peer (P2P) communication topology.

* **Formal Verification:** Integrating statistical model checking to ensure swarm safety and consensus guarantees.

* **Heterogeneous Swarm Support:** Enhancing map variables to better manage diverse robot types within a single script.

---

*For technical details refer to the full PiELo Final Paper: [https://digital.wpi.edu/concern/student_works/wd3761406?locale=en].*