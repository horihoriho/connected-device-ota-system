# CONCEPT

## Overview

### Background

Connected devices provide capabilities such as remote monitoring, remote control, and software updates through communication with remote servers. These capabilities are important components of connected systems used in various products, including IoT devices, industrial equipment, and medical devices.

To implement these capabilities, this project focuses on three key technical areas: bidirectional communication between a device and a server, asynchronous status and event notification, and remote software updates.

This project also aims to strengthen my practical implementation skills and deepen my understanding of connected device technologies by building a system in C++ on Linux, based on my previous experience with connected systems, communication protocols, and system development.

### Purpose 
The purpose of this system is to implement a simplified connected device environment that supports remote device monitoring, remote control, and software updates through network communication.

### System Architecture
 
                    ┌────────────────────────┐
                    │   Management Server    │
                    │                        │
                    │ TCP Command Server     │
                    │ MQTT Subscriber        │
                    │ OTA Package Server     │
                    └────────────────────────┘
                            │        │
                            │        │
                           TCP      OTA
                            │        │
                            ▼        ▼
                    ┌───────────────────────┐
                    │   Connected Device    │
                    │      C++ / Linux      │
                    │                       │
                    │ TCP Command Client    │
                    │ MQTT Publisher        │
                    │ OTA Manager           │
                    └───────────────────────┘
                               │
                              MQTT
                               │
                               ▼
                         ┌─────────────┐
                         │ MQTT Broker │
                         └─────────────┘

## Use Cases

The system implements the following three primary use cases:

1. **Device Monitoring**  
   The device periodically reports its status to the server and also sends notifications when specific events occur, allowing the management side to monitor the latest device state.

2. **Remote Control**  
   The server sends control commands to the device. The device executes the requested command and returns the execution result to the server.

3. **Software Update**  
   The server initiates a software update. The device retrieves the update package, verifies it, applies the update, and reports the update result.

## Scope

The project implements the device and server components within the following scope.

### Device

- C++ application running on Linux
- Remote command reception and response using TCP/IP
- Device status and event notification using MQTT
- OTA package retrieval, verification, and update installation
- Basic error handling for communication failures, timeouts, and other failure scenarios

### Server

- Simple device management system running on Linux
- Remote command transmission and response reception using TCP/IP
- Device status and event monitoring using MQTT
- OTA package distribution

### Out of Scope

Security mechanisms such as TLS, device authentication, and cryptographic signature verification of OTA packages are outside the scope of the initial implementation.

However, the system architecture should allow these security mechanisms to be introduced as future extensions.
