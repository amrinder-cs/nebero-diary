
# Week 4 Summary

## Compilation on ARM Based Systems

### Cross-Compiling Challenges
- Initial attempts to cross-compile for ARM without an ARM machine were unsuccessful.
- Architecture-independent code faced issues due to missing libraries.
- Manual installation of libraries via `.deb` files was not feasible.

### ARM Virtual Machine Setup
- GitHub hosted runners lacked ARM machines.
- Attempted to use VMware and VirtualBox with ARM ISO from Debian, but ARM architecture was unsupported.
- Successfully set up ARM virtual machine using Qemu and virt-manager.

## Network Connection Management Diary - 3rd September

### Code Improvements
- Refactored code to adhere to object-oriented programming standards.
- Introduced a `Packet` class for easier processing.
- Conducted tests to ensure correct hostname insertion.

### Key Components and Functions
- Detailed explanation of included libraries, global variables, and functions.
- Functions for managing connections, parsing TLS Client Hello messages, and database operations.

## Introduction to Deep Packet Inspection - 4th September

### Exploring DPI Techniques
- Investigated DPI for network management, security, and monitoring.
- Installed Netify agent to evaluate its performance.

### Limitations and Custom Plugin Development
- Discovered closed-source plugins and privacy concerns with Netify.
- Decided to develop a custom plugin for better control and security.

## Netify Plugins Exploration - 5th September

### Plugins Overview
- **Proc Core Plugin**: Captures network data in JSON format.
- **Socket Sink Plugin**: Facilitates real-time communication via `.sock` file.

### Implementation in C++
- Read socket file and parsed JSON data using the nlohmann/json library.
- Provided example code for parsing JSON data.

## Netify Information - 6th September

### Starting Netify
- Command to start Netify: `netifyd -R -v -t -r -I wlp3s0`.

### Flow Stats Information
- Explained local and other nomenclature.
- Provided example of flow stats and their significance.

