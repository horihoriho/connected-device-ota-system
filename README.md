# Connected Device OTA System

A personal engineering project to develop an Over-the-Air (OTA) software update and remote device management system.

This project focuses on **systems engineering**, covering the complete development lifecycle from requirements definition and system architecture design to implementation, testing, and verification.

**Status: In Progress — System Design**

## 1. Project Overview

The system is designed to manage a connected device remotely through three main functions:

- **Remote Monitoring:** Collect and report device health and software information.
- **Remote Control:** Receive and execute remote control commands.
- **OTA Software Update:** Check for available software updates, download and verify update packages, apply updates, and report results.

## 2. System Architecture

The system consists of four main components:

| Component | Responsibility |
|---|---|
| Connected Device | Collects status information, executes remote commands, and performs OTA updates |
| Management Server | Manages device monitoring, remote control, and update information |
| MQTT Broker | Exchanges monitoring messages between the device and server |
| OTA Package Server | Provides software update packages for download |

### Communication Protocols

| Protocol | Purpose |
|---|---|
| MQTT | Periodic and on-demand device monitoring |
| TCP | Remote control and OTA management messages |
| HTTP | OTA software package downloads |

## 3. Technology Stack

| Component | Technology |
|---|---|
| Connected Device | Raspberry Pi 4, C++, Linux |
| Management Server | Python |
| MQTT Broker | Mosquitto |
| Data Format | JSON |
| Version Control | Git / GitHub |

*The technology stack reflects the current design and may be updated during implementation.*

## 4. Development Approach

The project follows a systems engineering approach:

1. **Concept Definition** — Define project objectives, scope, and system capabilities.
2. **Requirements Definition** — Specify system and component requirements.
3. **System Design** — Define architecture, component responsibilities, and communication interfaces.
4. **Detailed Design** — Specify software behavior and implementation details.
5. **Implementation** — Develop the connected device and supporting server components.
6. **Verification** — Test system functions against the defined requirements.

## 5. Documentation

Design documentation is organized by development phase.

```text
docs/
├── 01_concept/
├── 02_requirements/
├── 03_architecture/
├── 04_detailed_design.md
└── 05_valification.md
```

Detailed design and verification documentation will be expanded as development progresses.

## 6. Current Progress

- [x] Project concept definition
- [x] Requirements definition
- [ ] System and communication design
- [ ] Detailed design
- [ ] Implementation
- [ ] Verification

## 7. Future Work

- Complete the TCP and HTTP communication designs.
- Define detailed software behavior and error handling.
- Implement device and server applications.
- Conduct functional and failure-handling tests.
- Document verification results and lessons learned.
