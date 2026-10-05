# Suricata IDS Deployment and Log Retention

## Project Overview

This project documents the deployment, monitoring, storage management, and log-retention engineering of a Suricata Intrusion Detection System (IDS) used for network traffic visibility.

The project evolved from an operational storage challenge caused by high-volume IDS event logging and resulted in a dedicated storage and retention strategy designed to maintain continuous event collection while controlling disk consumption.

All environment-specific information has been sanitized for public documentation.

---

## Objectives

* Provide network traffic visibility using Suricata IDS.
* Collect and analyze IDS security events.
* Integrate Suricata telemetry with centralized monitoring.
* Investigate high-volume log generation.
* Prevent uncontrolled log-storage growth.
* Provide dedicated storage for Suricata logs.
* Implement automated log rotation and compression.
* Establish a 180-day log-retention strategy.
* Validate that log collection continues normally after storage changes.

---

## Environment

### Suricata

* Suricata version: **7.0.3**
* Deployment: Virtual machine
* vCPU: **4**
* Memory: approximately **7.6 GiB**
* Network monitoring interfaces:

  * Monitoring interface connected to a SPAN/mirrored traffic source
  * Additional interface connected to the firewall/network path
* IDS traffic included multiple production VLANs.

### Monitoring

Suricata event data was collected by a centralized Wazuh monitoring environment.

The primary Suricata event file was:

```text
/var/log/suricata/eve.json
```

The environment also previously generated:

```text
/var/log/suricata/fast.log
```

---

## Initial Problem

The primary operational issue was uncontrolled growth of Suricata log files.

The `eve.json` event stream generated a very large volume of data because Suricata was continuously processing mirrored network traffic.

During investigation, the Suricata log directory had grown to approximately:

* **916 GB total**
* `eve.json`: approximately **743 GB**
* `fast.log` and rotated/compressed historical logs: approximately **162 GB**

The investigation showed that the issue was not simply the amount of available disk space. The logging and retention strategy itself needed to be improved.

---

## Investigation

The investigation focused on:

1. Identifying which Suricata files were consuming storage.
2. Determining the event volume being generated.
3. Checking whether log collection was still required.
4. Reviewing the relationship between Suricata logging and Wazuh collection.
5. Evaluating dedicated storage requirements.
6. Designing a controlled retention policy.
7. Validating Suricata configuration before and after changes.

A key observation was that the high-volume `eve.json` file was being actively consumed by the monitoring pipeline.

Therefore, simply deleting or disabling event logging without understanding the collection process could have resulted in loss of security telemetry.

---

## Storage Solution

A dedicated approximately **1 TB HDD** was added for Suricata log storage.

The disk was formatted using **ext4** and mounted specifically for:

```text
/var/log/suricata
```

This separated Suricata's high-volume logging workload from the operating system storage.

After cleanup and migration of the logging workload, the filesystem had approximately:

* **12 GB used**
* **858 GB available**

This provided substantially more operational headroom for continued event collection.

---

## Logging Configuration

The Suricata configuration was reviewed to reduce unnecessary log volume while preserving useful security telemetry.

The high-volume `fast.log` output was disabled.

The EVE JSON alert logging remained enabled because it provides structured event data suitable for centralized monitoring.

Selected EVE alert settings included:

```yaml
tagged-packets: no
verdict: yes
```

The configuration was validated using:

```bash
sudo suricata -T
```

The configuration test completed successfully.

Warnings concerning previously defined cluster/defragmentation settings were observed, but they did not prevent successful configuration validation or normal Suricata operation.

---

## Log Rotation and Retention

A log rotation strategy was implemented using Linux `logrotate`.

The retention design was changed to:

* Daily rotation
* **180 rotations**
* Date-based filenames
* Compression of rotated logs
* `copytruncate` handling where required
* Automated deletion of logs beyond the configured retention period

The objective is to maintain approximately **180 days of historical Suricata logs** while preventing indefinite disk growth.

The retention mechanism is designed to operate automatically rather than relying on manual cleanup.

---

## Validation

After the storage and logging changes were implemented, the system was monitored to verify normal operation.

Validation included:

### Configuration validation

```bash
sudo suricata -T
```

Result:

```text
Configuration test completed successfully.
```

### Service validation

The Suricata process remained active after the configuration and storage changes.

### Log-growth validation

After approximately ten minutes of normal operation, the `eve.json` file continued to receive new events.

A sample observation showed growth from approximately:

```text
2.8 MB
```

to approximately:

```text
111 MB
```

during the observation period.

This confirmed that Suricata continued generating events after the changes.

### Event validation

A sample event review showed approximately:

* **153,755 alert events**
* **79 statistics events**
* **74 anomaly events**

This confirmed continued event generation and visibility.

Alert Analysis

One of the frequently observed alerts was:

STREAM ESTABLISHED packet out of window

The observed traffic was associated with a NAS/service communication pattern.

This highlighted an important operational point:

An IDS alert should be investigated in the context of the application, traffic flow, and network behavior rather than automatically treated as a confirmed security incident.

The alert investigation therefore becomes part of ongoing IDS tuning and operational monitoring.

Monitoring Integration

Suricata event data is monitored through centralized Wazuh infrastructure.

The architecture provides a workflow similar to:

Network Traffic
      |
      v
SPAN / Mirrored Traffic
      |
      v
Suricata IDS
      |
      v
EVE JSON Events
      |
      v
Centralized Monitoring
      |
      v
Security Events / Dashboards / Investigation

This allows network-level detection data to be correlated with other infrastructure security telemetry.

Engineering Decisions
Dedicated storage

Dedicated storage was selected because Suricata generates a high volume of continuous telemetry.

Structured EVE logging

EVE JSON was retained because structured events are useful for centralized monitoring and analysis.

Disable unnecessary duplicate logging

fast.log was disabled to reduce unnecessary storage consumption while retaining the structured event stream.

Automated retention

Manual deletion was avoided in favor of an automated retention policy.

Validation before and after changes

Configuration testing and post-change monitoring were used to verify that the IDS remained operational.

Lessons Learned
1. IDS storage requirements must be measured from actual traffic

Storage planning should be based on observed event-generation rates rather than simply estimating disk requirements.

2. Log retention is part of system design

Security monitoring is not complete when logs are generated. Retention, rotation, compression, and deletion must also be engineered.

3. High-volume logs require dedicated storage planning

Separating high-volume security telemetry from operating-system storage provides better operational control.

4. Never remove logging without understanding the monitoring pipeline

Because Suricata events were being consumed by centralized monitoring, changes to logging required validation to avoid unintentionally losing security telemetry.

5. Post-change validation is essential

A configuration that passes a syntax test is not enough. Continued event generation and service health must also be verified.

Security Considerations

This public case study intentionally excludes:

Real IP addresses
Real hostnames
Real domains
Public IP addresses
MAC addresses
Credentials
API keys
VPN secrets
Organization-specific security policies
Sensitive production logs
Personally identifiable information

The technical concepts and engineering methodology are preserved while environment-specific information is sanitized.

Technologies
Suricata 7.0.3
Wazuh
Linux / Ubuntu Server
EVE JSON
SPAN / mirrored network traffic
ext4
logrotate
Log compression
IDS event analysis
Storage capacity planning
Security monitoring
Project Outcome

The project established a controlled Suricata logging architecture with:

Dedicated log storage
Reduced unnecessary log output
Structured security-event collection
Automated log rotation
Compression of historical logs
Automated 180-day retention
Configuration validation
Continued event generation after implementation

The result is a more sustainable IDS logging architecture that balances security visibility, storage capacity, operational reliability, and long-term retention.
---
