# Requirements

## System Requirements

The system requirements are defined as follows.

| Requirements | details |
| ------------ | ---------------------------------- |
| SYS-RM-001 | The system shall support periodic monitoring of connected device status. |
| SYS-RM-002 | The system shall support on-demand monitoring of connected device status. |
| SYS-RC-001 | The system shall support remote control of connected device. |
| SYS-OTA-001 | The system shall support remote software updates for connected device. |
| SYS-OTA-002 | The system shall provide the result of software updates. |


## Device Requirements

The device requirements are defined as follows.

| Requirements | details |
| ------------ | ---------------------------------- |
| DEV-RM-001 | The device shall collect its status periodically. The status shall include Device ID, Software Version, Uptime, CPU Temperature, CPU Usage, Memory Usage, and Timestamp. |
| DEV-RM-002 | The device shall indicate that the device status is unavailable until the initial status collection is completed. |
| DEV-RM-003 | The device shall periodically send its latest status to the server. |
| DEV-RM-004 | The device shall receive an on-demand device status request from the server. |
| DEV-RM-005 | The device shall send its latest status to the server in response to the on-demand status request from the server. |
| DEV-RM-006 | The device shall retry sending status when it fails. |
| DEV-RM-007 | The device shall retain only the latest status for monitoring. |
| DEV-RM-008 | The device shall send the device status even when one or more status values are unavailable. |
| DEV-RC-001 | The device shall receive the remote control request from the server. |
| DEV-RC-002 | The device shall report that the remote control request cannot be executed when the received request cannot be executed. |
| DEV-RC-003 | The device shall retry the remote control operation when the execution fails. |
| DEV-RC-004 | The device shall send the result of remote control to the server. |
| DEV-RC-005 | The device shall retry sending the remote control result when it fails. | 
| DEV-OTA-001 | The device shall request software update information to the server at startup. The request shall include the current software version. |
| DEV-OTA-002 | The device shall receive software update information from the server. |
| DEV-OTA-003 | The device shall retry the software update information request when it fails. |
| DEV-OTA-004 | The device shall obtain the OTA package from the OTA package server. |
| DEV-OTA-005 | The device shall retry downloading the OTA package when it fails. |
| DEV-OTA-006 | The device shall retry the OTA process at the next startup if the retry fails. |
| DEV-OTA-007 | The device shall verify the OTA package. |
| DEV-OTA-008 | The device shall discard the OTA package and abort the OTA process when verification fails. |
| DEV-OTA-009 | The device shall apply the OTA package. |
| DEV-OTA-010 | The device shall retry applying the OTA package when the application fails. |
| DEV-OTA-011 | The device shall verify the updated software version. |
| DEV-OTA-012 | The device shall send the OTA result to the server. | 
| DEV-OTA-013 | The device shall retry sending the OTA result when it fails. |


## Server Requirements

The server requirements are defined as follows.

| Requirements | details |
| ------------ | ---------------------------------- |
| SVR-RM-001 | The server shall receive periodic device status from the device. |
| SVR-RM-002 | The server shall send an on-demand device status request to the device. |
| SVR-RM-003 | The server shall receive on-demand device status from the device. |
| SVR-RC-001 | The server shall send the remote control request to the device. |
| SVR-RC-002 | The server shall receive the result of remote control from the device. |
| SVR-OTA-001 | The server shall receive a software update information request from the device. |
| SVR-OTA-002 | The server shall determine whether an update is available and send update information to the device. |
| SVR-OTA-003 | The server shall provide the OTA package to the device. |
| SVR-OTA-004 | The server shall receive the OTA result from the device. |

