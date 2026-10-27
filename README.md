# Wazuh SIEM Home Lab — File Integrity Monitoring

## Project Overview

This project demonstrates a hands-on Security Information and Event Management (SIEM) home lab using Wazuh. The lab monitors a Windows endpoint and detects file changes using File Integrity Monitoring (FIM).

The objective is to understand endpoint monitoring, security event collection, alert generation, centralized indexing, and troubleshooting in a security monitoring environment.

## Lab Environment

- **SIEM:** Wazuh 4.14.9
- **Server OS:** Ubuntu Server 24.04 LTS
- **Endpoint OS:** Windows 11
- **Components:** Wazuh Manager, Wazuh Indexer, Wazuh Dashboard, Wazuh Agent, Filebeat
- **Monitoring feature:** File Integrity Monitoring (FIM)

## Architecture

Windows Endpoint → Wazuh Agent → Wazuh Manager → Filebeat → Wazuh Indexer → Wazuh Dashboard

## Key Implementations

- Deployed a Wazuh single-node SIEM environment.
- Connected a Windows endpoint to the Wazuh Manager.
- Configured FIM to monitor a dedicated test directory.
- Tested file creation and deletion to generate security alerts.
- Inspected Wazuh alert records to verify event detection.
- Troubleshot agent connectivity, Filebeat service failures, and missing registry metadata.
- Verified Wazuh Indexer cluster health.

## FIM Testing

Test directory:

`C:\Users\khush\Downloads\wazuh-test`

Example test cases:

| Activity | Expected detection |
|---|---|
| Create a text file | File added alert |
| Delete a monitored file | File deleted alert |
| Modify a monitored file | File modification alert, when applicable |

The Wazuh manager's `alerts.json` was verified to contain file-added and file-deleted events from the Windows agent.

## Troubleshooting Experience

During implementation, the Windows agent initially used an incorrect Manager IP address. After correcting the connection target, the agent became active.

Filebeat also failed to start because its registry metadata file was missing. I inspected the service status and registry directory, backed up the existing registry directory, and restarted Filebeat successfully.

These troubleshooting steps helped me understand the event flow between the endpoint, manager, indexer, and dashboard.

## Skills Demonstrated

- SIEM deployment and configuration
- Endpoint security monitoring
- File Integrity Monitoring
- Windows and Linux administration
- Log analysis and alert validation
- Network connectivity troubleshooting
- Service and registry troubleshooting
- Basic security event investigation

## Evidence and Screenshots

Add screenshots demonstrating:

1. Wazuh dashboard showing the Windows agent as Active.
2. FIM configuration for the test directory.
3. File-added and file-deleted alerts in `alerts.json`.
4. Wazuh Indexer cluster health.
5. Filebeat service running successfully.
6. FIM events displayed in the dashboard after indexing is verified.

## Current Validation Status

Agent connectivity and FIM alert generation have been verified. The indexer health is green, and Filebeat has been restarted successfully. End-to-end indexing and dashboard visibility should be verified before considering the complete alert pipeline finished.

## Future Improvements

- Validate end-to-end alert indexing and dashboard visualization.
- Test file modification and hash changes.
- Monitor additional Windows directories.
- Explore security event correlation and custom detection rules.

## Disclaimer

This is a personal educational lab using a controlled test environment. Do not publish authentication keys, passwords, private certificates, or sensitive configuration data.
