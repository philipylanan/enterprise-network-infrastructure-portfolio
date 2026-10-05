# Hyper-V Replica

## Project Overview

This project documents the implementation, configuration, monitoring, and troubleshooting of Microsoft Hyper-V Replica for a critical virtual machine workload.

The solution provides asynchronous replication between Hyper-V hosts to improve recovery readiness in the event of a host or workload failure.

The project demonstrates practical experience with:

* Hyper-V Replica configuration
* Primary and replica host relationships
* Replication frequency configuration
* Kerberos-based replication
* Replica health monitoring
* Storage dependency analysis
* Replication troubleshooting
* Synchronization validation
* Recovery-point management
* Disaster-recovery readiness

---

## Objectives

The primary objectives were to:

* Provide replication for a critical virtual machine
* Establish a replica on a separate Hyper-V host
* Configure an appropriate replication interval
* Monitor replication health
* Validate synchronization behavior
* Identify dependencies affecting replica health
* Troubleshoot replication issues systematically
* Maintain recovery readiness without exposing production configuration details

---

## Hyper-V Replica Architecture

The environment uses a primary Hyper-V host and a separate replica Hyper-V host.

A simplified architecture is:

```text
                 Production Network
                        |
                        |
              Primary Hyper-V Host
                        |
                 Critical VM
                        |
                  Hyper-V Replica
                        |
                Replication Network
                        |
                        v
              Replica Hyper-V Host
                        |
                   Replica VM
```

The replica host maintains a synchronized copy of the protected virtual machine.

---

## Replication Configuration

The protected workload was configured with:

* A designated primary Hyper-V host
* A designated replica Hyper-V host
* Hyper-V Replica
* Kerberos-based authentication
* A configured replication frequency
* Replica health monitoring
* Recovery-point management

The configured replication interval for the protected workload was **5 minutes**.

The replication configuration was designed to provide a balance between recovery-point objectives, network utilization, storage requirements, and workload requirements.

---

## Authentication and Connectivity

The replication relationship used Kerberos-based authentication.

Successful replication therefore depends on more than the Hyper-V Replica configuration itself.

Validation included consideration of:

* Host-to-host network connectivity
* Authentication requirements
* Name resolution
* Firewall connectivity
* Hyper-V Replica configuration
* Availability of the replica host

A connectivity problem at the infrastructure layer can result in replication health problems even when the virtual machine configuration itself is correct.

---

## Replica Storage Requirements

Storage is a critical dependency of Hyper-V Replica.

The replica environment requires sufficient storage for:

* Replica virtual machine disks
* Recovery points
* Replication changes
* Temporary replication activity
* Future workload growth

Storage conditions were therefore included in the replication troubleshooting process.

This was particularly important when replication health changed following storage-related activity.

---

## Replica Health Monitoring

Hyper-V Replica health was monitored using Hyper-V management tools and replication status information.

Validation included:

* Replication state
* Last synchronization
* Replication health
* Replica host availability
* Storage availability
* Network connectivity
* Authentication/connectivity requirements
* Recovery-point availability

The objective was to determine whether the replica was actively synchronizing rather than relying solely on the existence of a configured replication relationship.

---

## Replication Health Issue Investigation

During operational validation, the replica relationship reported a critical health condition following storage-related activity.

The investigation considered multiple possible dependencies rather than immediately modifying the replication configuration.

The troubleshooting process examined:

```text
Replication Health
       |
       +---- Host Availability
       |
       +---- Network Connectivity
       |
       +---- Authentication
       |
       +---- Storage Availability
       |
       +---- VM Configuration
       |
       +---- Synchronization State
```

This approach helped separate configuration problems from underlying infrastructure conditions.

---

## Troubleshooting Methodology

Hyper-V Replica troubleshooting followed a layered process.

### 1. Replication Configuration

Verify:

* Primary host
* Replica host
* Protected VM
* Replication frequency
* Authentication method
* Recovery-point configuration

### 2. Host Health

Check:

* Hyper-V services
* CPU utilization
* Memory utilization
* Storage availability
* Windows event logs
* Network adapter status

### 3. Network Connectivity

Check:

* Host-to-host connectivity
* Name resolution
* Firewall requirements
* Replication communication
* Virtual and physical network paths

### 4. Storage

Check:

* Available capacity
* Replica storage
* VM disk availability
* Storage health
* Storage performance
* Capacity for ongoing replication

### 5. Synchronization

Check:

* Last successful synchronization
* Current replication state
* Replication health
* Pending changes
* Recovery points

This layered methodology reduces the risk of making unnecessary changes to a working replication configuration.

---

## Validation

Operational validation included:

* Reviewing the Hyper-V Replica relationship
* Confirming the protected VM
* Confirming the replica host
* Checking replication frequency
* Reviewing synchronization status
* Reviewing replica health
* Checking storage availability
* Checking network connectivity
* Reviewing Windows and Hyper-V event information

Validation was performed using both configuration information and observed operational status.

---

## Recovery Considerations

Hyper-V Replica provides a recovery mechanism but does not replace a complete backup strategy.

The solution was considered as part of a broader recovery architecture.

Recovery planning should account for:

* Replica availability
* Recovery-point age
* Storage availability
* Application consistency
* Network availability
* DNS and authentication dependencies
* Backup availability
* Recovery procedures
* Post-recovery validation

A healthy replica should therefore be treated as one component of disaster-recovery readiness rather than as the only recovery mechanism.

---

## Engineering Decisions

### Separate Replica Host

A separate Hyper-V host was used to avoid placing the primary and replica workloads on the same host.

### Five-Minute Replication

A five-minute replication interval was configured for the protected workload based on its recovery requirements.

### Kerberos Authentication

Kerberos-based replication was used within the Windows infrastructure environment.

### Health-Based Validation

Replication health was checked using synchronization and health information rather than assuming that a configured relationship was healthy.

### Storage-Aware Troubleshooting

Storage availability was treated as a first-class dependency during replication troubleshooting.

### Evidence Before Change

Replication problems were investigated using configuration, host, network, storage, and synchronization evidence before making corrective changes.

---

## Lessons Learned

Key lessons from the project include:

* Hyper-V Replica depends on healthy host, network, authentication, and storage infrastructure.
* A configured replication relationship does not automatically guarantee healthy synchronization.
* Storage conditions can directly affect replication health.
* Replication status should be monitored continuously.
* Troubleshooting should proceed from configuration to infrastructure dependencies.
* Recovery-point availability is an important part of replication validation.
* Replication should complement rather than replace backup and recovery procedures.
* Configuration changes should always be followed by operational validation.

---

## Security Considerations

The public version of this project intentionally excludes:

* Production IP addresses
* Production hostnames
* Internal domain names
* VM names
* Credentials
* Authentication secrets
* Certificates
* MAC addresses
* Exact VLAN mappings
* Firewall rules
* Storage identifiers
* Recovery credentials
* Sensitive replication configuration
* Organization-specific operational information

The documentation focuses on the engineering methodology and technologies used rather than exposing the production recovery environment.

---

## Technologies

* Microsoft Windows Server 2025
* Hyper-V
* Hyper-V Replica
* Hyper-V Manager
* Kerberos
* Windows networking
* Enterprise storage
* Windows Event Viewer
* PowerShell
* Disaster recovery
* Business continuity

---

## Project Outcome

The Hyper-V Replica implementation provides a recovery-oriented replication capability for a critical virtual machine workload.

The project demonstrates practical experience with:

* Designing a primary/replica relationship
* Configuring replication
* Selecting an appropriate replication interval
* Monitoring synchronization
* Investigating replica health
* Troubleshooting storage and connectivity dependencies
* Validating recovery readiness
* Documenting disaster-recovery infrastructure

The project reinforces the importance of **continuous health monitoring, storage awareness, evidence-based troubleshooting, and validation of actual replication behavior**.
