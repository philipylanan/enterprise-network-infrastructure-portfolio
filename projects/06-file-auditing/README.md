# File Auditing and Security Monitoring

## Project Overview

This project documents the implementation of centralized file-activity auditing and security monitoring for Windows file-server infrastructure.

The solution was designed to provide visibility into important file-system activity, including **file creation, modification, and deletion**, while centralizing security telemetry through Wazuh.

The implementation combined Windows security auditing, SACL-based auditing, PowerShell-based operational support, and centralized event monitoring.

All environment-specific information has been sanitized for public documentation.

---

## Objectives

* Monitor important file-system activity.
* Detect file creation, modification, and deletion.
* Centralize file-audit security events.
* Integrate Windows file auditing with Wazuh.
* Provide searchable historical audit information.
* Support investigation of unexpected file activity.
* Establish appropriate audit-event retention.
* Control audit-event volume and storage consumption.
* Validate that file auditing continues after configuration changes.

---

## Monitoring Architecture

The file-auditing workflow was designed as a layered monitoring process:

```text
Windows File Server
        |
        v
Windows Security Auditing
        |
        v
SACL-Based File Auditing
        |
        v
Windows Security Events
        |
        v
Wazuh Agent
        |
        v
Wazuh Manager
        |
        v
Security Events / Dashboards
        |
        v
Investigation
```

This architecture provided centralized visibility while allowing the file server to continue performing its normal file-service functions.

---

## Windows File Auditing

Windows security auditing was used to record relevant file-system activity.

The monitoring design included auditing for:

* **File creation**
* **File modification**
* **File deletion**
* **Object access**
* **Security-related file activity**

Auditing was implemented using Windows security auditing capabilities and SACL-based configuration.

SACLs were used to define which file-system access activity should generate security-audit events.

---

## SACL-Based Monitoring

System Access Control Lists (SACLs) were used to identify the file-system activities that required auditing.

The design considered:

* Objects requiring monitoring
* Access types requiring monitoring
* Successful access events
* Failed access events where applicable
* Event volume
* Security-investigation requirements
* Storage requirements

SACL configuration was designed to provide useful security visibility without unnecessarily auditing every possible operation.

Production paths, shares, server names, and organization-specific SACL configurations are intentionally excluded.

---

## File Activity Monitoring

The monitoring solution focused on file activities that were operationally important.

Examples included:

### **File Creation**

Creation events provided visibility when new files were introduced into monitored locations.

### **File Modification**

Modification events helped identify changes to existing files.

### **File Deletion**

Deletion events provided visibility into removal of files and supported investigation of unexpected or unauthorized deletion activity.

The objective was not simply to collect events, but to make the events useful for security investigation.

---

## PowerShell Operational Support

A PowerShell-based operational mechanism was used to support file-deletion auditing within the environment.

The mechanism assisted with generating or processing deletion-related information for centralized monitoring.

The actual production script, file paths, server names, and organization-specific implementation details are intentionally excluded from this public case study.

---

## Wazuh Integration

Wazuh was used as the centralized monitoring platform for Windows file-audit telemetry.

The integration provided:

* Centralized event collection
* Event searching
* Security-event analysis
* Dashboard visibility
* Historical investigation
* Correlation with other Windows security events

The overall monitoring path was:

```text
File Activity
      |
      v
Windows Security Event
      |
      v
Wazuh Agent
      |
      v
Wazuh Manager
      |
      v
Security Dashboard
      |
      v
Investigation
```

This reduced the need to manually review individual file-server event logs.

---

## Event Investigation

File-audit events were investigated using a structured process.

1. **Identify the affected file activity.**
2. **Review the event timestamp.**
3. **Identify the event type.**
4. **Determine the affected object.**
5. **Identify the associated user or security context.**
6. **Review related events.**
7. **Determine whether the activity was expected.**
8. **Correlate the activity with operational or application context.**
9. **Document findings where required.**

A file deletion event, for example, was treated as evidence requiring investigation rather than automatically being classified as malicious activity.

---

## Security Monitoring Use Cases

The file-auditing implementation supported several security and operational use cases.

### **Unauthorized File Activity**

Unexpected creation, modification, or deletion could be investigated through centralized security telemetry.

### **User Activity Investigation**

Audit events provided information that could help determine which security context was associated with an activity.

### **Operational Troubleshooting**

File-audit events could assist in understanding unexpected file changes affecting applications or users.

### **Security Incident Investigation**

File activity could be correlated with authentication, system, and network events when investigating a broader security event.

---

## Audit Event Volume

File auditing can generate substantial event volume depending on:

* Number of monitored files
* Number of users
* File-access frequency
* Application behavior
* Audited access types
* Security policy
* Monitoring scope

For this reason, auditing was designed around required visibility rather than enabling every possible audit category indiscriminately.

---

## Retention and Storage

File-audit retention was considered as part of the overall security-monitoring architecture.

Retention planning considered:

* Audit-event volume
* Storage capacity
* Investigation requirements
* Security importance
* Historical visibility
* Operational requirements
* Organizational retention requirements

File-audit data can have significant investigative value because historical activity may be required when determining how and when a file changed.

The retention strategy was therefore designed separately from high-volume network telemetry where appropriate.

---

## Validation

The file-auditing implementation was validated by checking that expected activity generated corresponding security telemetry.

Validation activities included:

* Confirming Windows audit configuration
* Checking SACL configuration
* Performing controlled file operations
* Reviewing generated Windows security events
* Confirming Wazuh agent collection
* Searching for expected events in Wazuh
* Reviewing dashboards
* Monitoring event volume
* Checking storage consumption

The objective was to verify the complete path from **file activity to centralized security visibility**.

---

## Troubleshooting Methodology

When file-audit events were missing or incomplete, troubleshooting followed the collection path.

1. **Confirm the file operation occurred.**
2. **Check Windows auditing configuration.**
3. **Check SACL configuration.**
4. **Review Windows Security Event Logs.**
5. **Check Wazuh agent status.**
6. **Check Wazuh collection configuration.**
7. **Review manager-side event ingestion.**
8. **Search for the expected event.**
9. **Check event volume and storage.**
10. **Validate again after corrective action.**

This approach helped identify whether an issue existed at the Windows auditing, SACL, agent, collection, ingestion, or storage layer.

---

## Engineering Decisions

### **Selective Auditing**

Audit scope was designed around useful security visibility rather than unrestricted auditing.

### **Centralized Collection**

Wazuh provided a centralized location for investigating file activity instead of relying exclusively on individual servers.

### **Security-Aware Retention**

Audit data was retained according to its investigative value and storage requirements.

### **Controlled Validation**

Configuration changes were validated using controlled file operations and verification of resulting security events.

### **Correlation With Other Telemetry**

File activity was considered alongside authentication, Windows security, network, and IDS telemetry when investigating broader events.

---

## Lessons Learned

### **1. File Auditing Must Be Designed Carefully**

Enabling excessive auditing can generate large event volumes and increase storage requirements.

### **2. SACL Configuration Directly Affects Visibility**

The quality of file-audit monitoring depends heavily on which objects and access types are selected for auditing.

### **3. Centralized Collection Simplifies Investigation**

Centralizing file-audit events makes historical investigation easier than manually reviewing individual servers.

### **4. File Events Require Context**

A file deletion or modification is not automatically malicious. User activity, application behavior, timing, and related events must be considered.

### **5. Retention Is Part of the Audit Design**

Collecting events without considering storage capacity and retention requirements can create operational problems.

### **6. End-to-End Validation Is Essential**

Successful configuration does not guarantee that events are reaching the monitoring platform. The entire collection path must be tested.

---

## Security Considerations

This public case study intentionally excludes:

* Real IP addresses
* Real hostnames
* Real domains
* Production file-server names
* Production share names
* Production file paths
* Usernames
* Credentials
* Security-policy details
* Production PowerShell scripts
* Sensitive audit records
* Personally identifiable information

The technical methodology is preserved while environment-specific information is sanitized.

---

## Technologies

* **Windows Server**
* **Windows Security Auditing**
* **SACL**
* **File-system auditing**
* **PowerShell**
* **Wazuh**
* **Windows Security Event Logs**
* **Centralized security monitoring**
* **Log retention**
* **Storage capacity planning**
* **Security-event investigation**

---

## Project Outcome

The file-auditing implementation established centralized visibility into important Windows file-system activity.

The resulting monitoring capability provided:

* **File creation monitoring**
* **File modification monitoring**
* **File deletion monitoring**
* **SACL-based auditing**
* **Centralized Wazuh collection**
* **Security-event investigation**
* **Historical audit visibility**
* **Retention and storage planning**
* **End-to-end monitoring validation**

The project demonstrates practical security-monitoring engineering by combining **Windows auditing, centralized event collection, investigation methodology, retention planning, and operational validation**.
