# Requirements

## System Requirements

| Requirements | details |
| ------------ | ---------------------------------- |
| SYS-RM-001 | The system shall support periodic monitoring of connected device status. |
| SYS-RM-002 | The system shall support on-demand monitoring of connected device status. |
| SYS-RC-001 | The system shall support remote control of connected device. |
| SYS-OTA-001 | The system shall support remote software updates for connected device. |
| SYS-OTA-002 | The system shall provide the result of software updates. |


## Device Requirements

| Requirements | details |
| ------------ | ---------------------------------- |
| DEV-RM-001 | The device shall collect its status periodically. The status shall include Device ID, Software Version, Uptime, CPU Temperature, CPU Usage, Memory Usage, and Timestamp. |
| DEV-RM-002 | The device shall indicate that the device status is unavailable until the initial status collection is completed. |
| DEV-RM-003 | The device shall periodically send its latest status to the server. |
| DEV-RM-004 | The device shall receive the request to uploading on-demand status from the server. |
| DEV-RM-005 | The device shall send its latest status to the server in response to the on-demand status request from the server. |
| DEV-RM-006 | The device shall retry sending status when it is failed. |
| DEV-RM-007 | The device shall retain only the latest status for monitoring. |
| DEV-RM-008 | The device shall send the device status even when one or more status values are unavailable. |
| DEV-RC-001 | The device shall receive the remote control request from the server. |
| DEV-RC-002 | The device shall report that the remote control request cannot be executed when the received request cannot be executed. |
| DEV-RC-003 | The device shall retry the remote control operation when the execution fails. |
| DEV-RC-004 | The device shall send the result of remote control to the server. |
| DEV-RC-005 | The device shall retry sending of the remote control result when it is failed. | 
| DEV-OTA-001 | The device shall receive the OTA execution notification from the server. |
| DEV-OTA-002 | The device shall obtain the OTA package from the OTA package server. |
| DEV-OTA-003 | The device shall verify the OTA package. |
| DEV-OTA-004 | The device shall apply the OTA package. |
| DEV-OTA-005 | The device shall send the OTA result to the server. | 


## Server Requirements

| Requirements | details |
| ------------ | ---------------------------------- |
| SVR-RM-001 | The server shall receive periodic device status from the device. |
| SVR-RM-002 | The server shall receive on-demand device status from the device. |
| SVR-RM-003 | The server shall send the request to uploading on-demand device status to the device. |
| SVR-RC-001 | The server shall send the remote control request to the device. |
| SVR-RC-002 | The server shall receive the result of remote control from the device. |
| SVR-OTA-001 | The server shall send the OTA execution notification to the device. |
| SVR-OTA-002 | The server shall provide the OTA package to the device. |
| SVR-OTA-003 | The server shall receive the OTA result from the device. |

