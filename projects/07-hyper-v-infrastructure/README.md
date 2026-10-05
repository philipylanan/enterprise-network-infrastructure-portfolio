# Hyper-V Infrastructure

## Project Overview

This project documents the design, administration, validation, and operational management of a Windows Server Hyper-V virtualization environment supporting enterprise application, database, file, and infrastructure workloads.

The environment includes multiple Hyper-V hosts running Windows Server 2025 and a collection of production virtual machines with dedicated resource allocations, virtual networking, storage, and replication requirements.

The project demonstrates practical experience in:

* Hyper-V host administration
* Virtual machine deployment and resource allocation
* Virtual CPU and memory planning
* Hyper-V virtual switch configuration
* VLAN-aware virtual networking
* Storage and VM placement
* Hyper-V Replica
* VM health and replication validation
* Troubleshooting virtualization infrastructure
* Operational documentation

---

## Objectives

The primary objectives were to:

* Maintain reliable Hyper-V virtualization infrastructure
* Provide appropriate CPU and memory resources to critical workloads
* Maintain controlled virtual network segmentation
* Support production application and database workloads
* Implement VM replication for disaster-recovery requirements
* Validate VM and host health
* Troubleshoot virtualization and replication issues
* Maintain accurate technical documentation

---

## Virtualization Platform

The environment uses:

* Microsoft Windows Server 2025
* Hyper-V
* Hyper-V Manager
* Hyper-V Replica
* Windows virtual networking
* VLAN-aware virtual switches
* Enterprise server storage

The Hyper-V hosts provide the compute, memory, storage, and networking resources required by multiple production workloads.

---

## Hyper-V Host Architecture

The environment consists of multiple Windows Server Hyper-V hosts.

A simplified architecture is:

```text
                    Enterprise Network
                           |
                    Core / Firewall
                           |
                 ---------------------
                 |                   |
          Hyper-V Host A       Hyper-V Host B
                 |                   |
        -------------------   -------------------
        |        |        |   |       |       |
       VM      VM       VM   VM      VM      VM
        |
   Application /
   Database /
   Infrastructure
   Workloads
```

The virtualization architecture separates host-level infrastructure from the individual guest workloads while maintaining controlled connectivity through Hyper-V virtual switches.

---

## Virtual Machine Resource Management

Virtual machines were configured with workload-specific resource allocations.

Resource planning considered:

* Number of virtual CPUs
* Assigned memory
* Static versus dynamic memory requirements
* Application workload characteristics
* Database workload requirements
* Host resource availability
* Performance requirements
* Disaster-recovery requirements

Critical workloads were assigned larger resource allocations based on their operational requirements.

Resource allocation was reviewed against actual workload requirements rather than assigning identical resources to every virtual machine.

---

## Virtual Networking

Hyper-V virtual switches provide connectivity between virtual machines and the physical enterprise network.

The environment includes external and internal virtual switching configurations.

A simplified model is:

```text
                 Physical Network
                        |
                 Physical NICs
                        |
                Hyper-V Virtual Switch
                        |
        --------------------------------
        |              |               |
      VLAN A         VLAN B          VLAN C
        |              |               |
       VM             VM              VM
```

Virtual networking was designed to support:

* VLAN segmentation
* Production network connectivity
* Infrastructure services
* Application workloads
* Database workloads
* Management connectivity
* DMZ or isolated workloads where required

Where VLAN trunking is used, allowed VLANs are explicitly controlled rather than permitting unrestricted network access.

---

## Virtual Switch Configuration

Hyper-V virtual switch configuration was validated to ensure:

* Correct switch type
* Correct physical NIC association
* Correct VLAN configuration
* Correct VM network adapter assignment
* Appropriate trunk or access behavior
* Expected connectivity to upstream network infrastructure

The virtual networking configuration was also reviewed during troubleshooting to distinguish between:

* Hyper-V configuration problems
* Guest operating system problems
* Physical network problems
* VLAN configuration problems
* Upstream switching problems

---

## Storage and Virtual Machines

Virtual machine storage was hosted on enterprise server storage designed to support production workloads.

Storage planning considered:

* VM disk capacity
* Workload performance
* Available host capacity
* Database requirements
* Backup and recovery requirements
* Replication requirements
* Future growth

Critical workloads were monitored for storage utilization and operational health.

Storage availability is particularly important for Hyper-V Replica because replication requires sufficient space for replica and recovery data.

---

## Hyper-V Replica

Hyper-V Replica was used to provide replication capability for a critical virtual machine.

The replication architecture is:

```text
              Primary Hyper-V Host
                       |
                  Production VM
                       |
                Hyper-V Replica
                       |
                       v
              Replica Hyper-V Host
                       |
                 Replica VM
```

The replica configuration included:

* A designated primary virtual machine
* A designated replica host
* Kerberos-based replication
* Configured replication frequency
* Replica health monitoring
* Recovery-point management

The configured replication interval for the production workload was **5 minutes**.

---

## Replica Health Validation

Hyper-V Replica health was monitored through Hyper-V management tools and replication status.

Validation included checking:

* Replication state
* Last synchronization
* Replication health
* Replica server availability
* Storage availability
* Network connectivity
* Authentication/connectivity requirements

An important operational lesson was that replication health can be affected by underlying storage conditions.

When storage conditions changed, replica health required additional validation rather than assuming that the replication relationship remained healthy.

---

## Virtual Machine Health Validation

Routine validation included:

### Host

* Hyper-V service status
* CPU utilization
* Memory utilization
* Storage availability
* Physical NIC status
* Virtual switch configuration
* Event logs

### Virtual Machines

* VM power state
* Assigned CPU and memory
* Virtual NIC connectivity
* VLAN configuration
* Disk availability
* Guest operating system health
* Application availability

### Replica

* Replication status
* Synchronization state
* Replica health
* Recovery-point availability
* Storage capacity

---

## Troubleshooting Methodology

Hyper-V troubleshooting follows a layered approach.

### 1. Host

Check:

* Hyper-V role
* Host resource utilization
* Services
* Storage
* Physical network adapters
* Windows event logs

### 2. Virtual Machine

Check:

* VM state
* CPU and memory allocation
* Virtual disks
* Virtual network adapters
* VLAN configuration
* Guest operating system

### 3. Network

Check:

* Virtual switch
* Physical NIC
* VLAN configuration
* Upstream switch connectivity
* Routing
* Firewall policies

### 4. Storage

Check:

* Available capacity
* Disk health
* VM disk availability
* Storage performance
* Replica storage requirements

### 5. Replication

Check:

* Replica configuration
* Authentication/connectivity
* Replication interval
* Synchronization status
* Replica health
* Storage availability

This layered process helps isolate whether an issue originates at the host, VM, network, storage, or replication layer.

---

## Configuration and Operational Validation

Validation was performed after configuration changes and during troubleshooting.

Examples include:

* Reviewing Hyper-V host configuration
* Reviewing VM settings
* Verifying virtual switch assignments
* Validating VLAN configuration
* Checking VM connectivity
* Checking available storage
* Reviewing Hyper-V event logs
* Reviewing replica health
* Confirming synchronization behavior

The objective was to validate actual operational behavior rather than relying only on configuration screens.

---

## Engineering Decisions

Several engineering principles were applied:

### Workload-Based Resource Allocation

CPU and memory resources were assigned according to workload requirements rather than using identical VM configurations.

### Controlled Virtual Networking

Only required network segments were made available to workloads.

### Replication for Critical Workloads

Hyper-V Replica was used where recovery requirements justified the additional infrastructure and storage requirements.

### Evidence-Based Troubleshooting

Problems were investigated using host state, VM configuration, networking, storage, event logs, and replication status before making changes.

### Validation After Changes

Configuration changes were followed by operational validation to confirm that the intended behavior was achieved.

---

## Lessons Learned

Key lessons from the environment include:

* VM resource allocation should be reviewed against actual workload requirements.
* Virtual networking problems can originate at several layers and should be isolated systematically.
* VLAN trunk configuration must be carefully controlled.
* Storage capacity is an important dependency for virtualization and replication.
* Hyper-V Replica health should be monitored continuously.
* A replication configuration can appear correct while still experiencing operational health problems.
* Changes affecting storage or networking should always be followed by replication validation.
* Documentation should record both the intended configuration and the observed operational state.

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
* Detailed production VLAN mappings
* Firewall rules
* Sensitive network topology
* Storage identifiers
* Recovery credentials
* Other organization-specific operational information

The documentation focuses on engineering practices and technologies rather than exposing the production environment.

---

## Technologies

* Microsoft Windows Server 2025
* Hyper-V
* Hyper-V Manager
* Hyper-V Replica
* VLAN
* Virtual switching
* Enterprise networking
* Enterprise storage
* Windows Event Viewer
* PowerShell
* Disaster recovery / business continuity concepts

---

## Project Outcome

The Hyper-V environment provides a centralized virtualization platform for production workloads while supporting:

* Workload consolidation
* Controlled virtual networking
* Resource management
* Enterprise application hosting
* Database hosting
* Infrastructure services
* Replication for critical workloads
* Operational monitoring
* Structured troubleshooting
* Disaster-recovery readiness

The project demonstrates practical experience administering and troubleshooting enterprise Hyper-V infrastructure with emphasis on **resource planning, networking, storage, replication, validation, and operational reliability**.
