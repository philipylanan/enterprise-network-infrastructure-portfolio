# Wazuh SIEM and Security Monitoring

## Project Overview

This project documents the deployment, configuration, monitoring, and operational use of Wazuh as a centralized security monitoring and log-analysis platform.

The implementation provides centralized collection of security telemetry from Windows and Linux infrastructure, including operating-system events, network security events, file activity, authentication activity, and IDS telemetry.

The project also demonstrates the practical engineering required to configure agents, define monitoring requirements, investigate collected events, and manage log-retention requirements.

All environment-specific information has been sanitized for public documentation.

---

## Objectives

* Centralize security-event collection from infrastructure systems.
* Monitor Windows and Linux systems through Wazuh agents.
* Collect and analyze Windows security events.
* Monitor file activity and file-system changes.
* Collect network authentication and VPN-related events.
* Integrate Suricata IDS telemetry with centralized monitoring.
* Provide security dashboards and event investigation capability.
* Establish appropriate log-retention requirements.
* Validate that security telemetry continues to be collected after configuration changes.

---

## Environment

### Wazuh Manager

The centralized Wazuh manager was deployed on:

* Ubuntu Server 24.04
* Wazuh version **4.14.5**
* Virtual-machine deployment

The manager was configured for centralized security-event collection and analysis.

Structured JSON event logging was enabled to support detailed event processing and investigation.

---

## Monitored Infrastructure

The Wazuh environment included agents covering multiple infrastructure roles.

Examples of monitored systems included:

* Windows file-server infrastructure
* Windows NPS/RADIUS infrastructure
* Active Directory domain controllers
* Suricata IDS infrastructure
* Other Windows and Linux infrastructure requiring centralized monitoring

The public documentation intentionally uses generic system descriptions instead of production hostnames and IP addresses.

---

## Windows Security Monitoring

Wazuh was used to collect and analyze Windows security telemetry from monitored servers.

This provided visibility into activities such as:

* User authentication
* Security events
* File activity
* Object creation and deletion
* System activity
* Network authentication events

The collected telemetry could then be investigated through centralized Wazuh dashboards and event searches.

---

## File Activity Monitoring

One of the monitoring use cases involved auditing activity on a Windows file-server environment.

The monitoring design included:

* Windows file auditing
* Security audit policy
* SACL-based monitoring
* File creation events
* File modification events
* File deletion events
* Centralized event collection through Wazuh

A PowerShell-based operational mechanism was also used in the environment to support file-deletion auditing.

For public documentation, the actual production paths, server names, shares, and organization-specific details have been removed.

---

## NPS / VPN Authentication Monitoring

Wazuh was also used to monitor Windows Network Policy Server (NPS) activity associated with authentication and VPN access.

Important Windows NPS events included:

* **Event ID 6272** — successful network-policy authentication
* **Event ID 6273** — failed network-policy authentication

These events provided useful visibility into authentication activity and allowed successful and unsuccessful access attempts to be investigated centrally.

The monitoring design treated these events as security telemetry rather than relying on manual review of individual servers.

---

## Active Directory Monitoring

Wazuh agents were deployed on Active Directory infrastructure to provide centralized visibility into Windows security events.

Monitoring supported investigation of:

* Authentication activity
* Security events
* Directory-service infrastructure activity
* System-level security events

The public case study does not disclose production domain names, server names, IP addresses, or other organization-specific information.

---

## Suricata Integration

Suricata IDS telemetry was integrated into the centralized Wazuh monitoring environment.

The primary Suricata event stream used structured EVE JSON data:

```text
/var/log/suricata/eve.json
```

This allowed network-level IDS events to be collected alongside other infrastructure security telemetry.

The monitoring workflow can be represented as:

```text
Network Traffic
      |
      v
Suricata IDS
      |
      v
EVE JSON Events
      |
      v
Wazuh Collection
      |
      v
Security Events
      |
      v
Dashboards / Investigation
```

This integration provided a centralized view of security events originating from both network traffic monitoring and infrastructure systems.

---

## Event Investigation

A key operational capability of the Wazuh deployment was the ability to investigate events centrally.

The investigation process included:

1. Identify the event source.
2. Review the event timestamp.
3. Examine the event type and severity.
4. Identify the affected system or service.
5. Review related events.
6. Determine whether the event represents expected or unexpected activity.
7. Correlate the event with network or system behavior.
8. Document findings and required action.

This approach helps prevent individual security events from being interpreted without sufficient operational context.

---

## Log Retention

Log retention was treated as part of the monitoring architecture rather than as an afterthought.

Retention requirements were evaluated according to:

* Event volume
* Security importance
* Available storage
* Operational investigation requirements
* Compliance or organizational requirements
* Storage growth rate

Different monitoring workloads can require different retention periods.

For example, file-audit and security-monitoring data may require longer historical retention than high-volume network telemetry.

Retention policies were therefore designed around the characteristics of each monitored workload.

---

## Storage and Capacity Considerations

Centralized security monitoring can generate substantial storage requirements.

The Wazuh implementation required consideration of:

* Daily event volume
* Index/storage growth
* Log retention
* Agent-generated telemetry
* Suricata event volume
* File-audit activity
* Authentication-event volume
* Available storage capacity

The engineering approach was to measure actual event generation and storage consumption rather than relying solely on theoretical estimates.

---

## Operational Validation

Wazuh monitoring was validated by checking whether expected telemetry was being received from monitored systems.

Validation activities included:

* Checking agent connectivity
* Reviewing incoming events
* Searching for expected Windows event IDs
* Reviewing file-audit activity
* Reviewing NPS authentication events
* Reviewing Suricata events
* Checking dashboards and event searches
* Monitoring storage consumption

The objective was to confirm that monitoring changes did not unintentionally interrupt security-event collection.

---

## Engineering Decisions

### Centralized monitoring

Centralizing security telemetry simplified event investigation and provided a common monitoring platform for multiple infrastructure systems.

### Agent-based collection

Wazuh agents were used where host-level visibility was required.

This provided access to operating-system and security events that could not be obtained from network monitoring alone.

### Structured event collection

Structured event data improved searchability and analysis and allowed different security telemetry sources to be investigated through a common platform.

### Integration with IDS telemetry

Integrating Suricata with Wazuh connected network-level detection with host and infrastructure security monitoring.

### Storage-aware monitoring design

Security monitoring was designed with storage consumption and retention requirements in mind.

---

## Lessons Learned

### 1. Monitoring must be designed around actual event volume

Security platforms can generate large amounts of telemetry. Capacity planning should use observed event rates whenever possible.

### 2. Centralized visibility improves investigation

Collecting events from multiple infrastructure systems makes it easier to correlate activity and investigate incidents.

### 3. Security events require operational context

A single event should not automatically be treated as a confirmed security incident. Event source, timing, application behavior, and related activity should be considered.

### 4. Retention is part of security monitoring

Generating security events is only one part of the monitoring architecture. Storage, retention, rotation, and historical investigation must also be considered.

### 5. Monitoring changes require validation

Configuration changes should be followed by checks confirming that agents remain connected and expected events continue to arrive.

---

## Security Considerations

This public case study intentionally excludes:

* Real IP addresses
* Real hostnames
* Real domains
* Public IP addresses
* MAC addresses
* Credentials
* API keys
* VPN secrets
* Organization-specific security policies
* Sensitive production logs
* Personally identifiable information

The technical concepts and engineering methodology are preserved while environment-specific information is sanitized.

---

## Technologies

* Wazuh 4.14.5
* Ubuntu Server 24.04
* Windows Server
* Windows Security Event Logging
* NPS / RADIUS
* Active Directory
* File auditing
* PowerShell
* Suricata IDS
* EVE JSON
* Security-event analysis
* Log retention
* Storage capacity planning
* Centralized security monitoring

---

## Project Outcome

The Wazuh implementation established a centralized security-monitoring capability covering multiple infrastructure workloads.

The resulting monitoring architecture provided:

* Centralized security-event collection
* Windows infrastructure monitoring
* File-activity monitoring
* NPS/VPN authentication visibility
* Active Directory security telemetry
* Suricata IDS integration
* Centralized dashboards and event investigation
* Storage and retention planning
* Operational validation of security telemetry

The project demonstrates the practical engineering required to operate a centralized security-monitoring platform while balancing visibility, storage, retention, and operational reliability.
