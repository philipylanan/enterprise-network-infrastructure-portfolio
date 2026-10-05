# Proxmox & Ceph Infrastructure

## Project Overview

This project documents hands-on administration and operational management of a **Proxmox VE virtualization environment with Ceph distributed storage** supporting enterprise infrastructure workloads.

The environment provides clustered virtualization, distributed storage, virtual machine lifecycle management, storage-aware workload placement, and infrastructure availability monitoring.

Production-specific IP addresses, hostnames, VM identifiers, storage identifiers, credentials, and other sensitive operational information have been sanitized.

---

## Objectives

* Administer a Proxmox VE virtualization cluster
* Manage virtual machines across multiple Proxmox nodes
* Operate and monitor Ceph distributed storage
* Validate cluster and storage health
* Manage VM placement and migration
* Understand the relationship between compute, virtualization, and distributed storage
* Support infrastructure services running as virtual machines
* Troubleshoot virtualization and storage-related issues
* Maintain operational documentation and validation procedures

---

## Virtualization Architecture

The infrastructure uses **Proxmox VE** as the virtualization platform.

A multi-node Proxmox cluster provides:

* Centralized virtualization management
* Multiple physical virtualization nodes
* Virtual machine lifecycle management
* VM placement across cluster nodes
* Storage integration
* Cluster-level health monitoring
* Migration capabilities
* Distributed storage through Ceph

### High-Level Architecture

```text
                    Enterprise Network
                           |
                           |
                  +-------------------+
                  |   Proxmox Cluster  |
                  +-------------------+
                     /      |       \
                    /       |        \
             +---------+ +---------+ +---------+
             | Node A  | | Node B  | | Node C  |
             +---------+ +---------+ +---------+
                  \          |          /
                   \         |         /
                    +------------------+
                    |   Ceph Storage   |
                    | Cluster / Pool   |
                    +------------------+
                           |
                    Virtual Machines
```

The diagram represents the architecture conceptually and does not expose production network addressing or infrastructure identifiers.

---

## Proxmox VE Administration

Hands-on administration included:

* Proxmox cluster management
* Node health monitoring
* VM creation and administration
* VM resource allocation
* VM lifecycle operations
* VM placement
* VM migration
* Virtual hardware management
* Virtual networking
* Storage assignment
* Cluster troubleshooting
* Operational validation

VM operations were performed with consideration for both compute resources and the underlying distributed storage architecture.

---

## Cluster Infrastructure

The Proxmox environment consists of multiple virtualization nodes operating as a cluster.

Cluster administration included validation of:

* Node availability
* Cluster membership
* Resource utilization
* VM distribution
* Storage connectivity
* Ceph health
* Cluster services
* VM operational state

A clustered architecture allows workloads to be managed across multiple physical virtualization hosts rather than relying on a single virtualization server.

---

## Ceph Distributed Storage

The virtualization environment uses **Ceph** as distributed storage for virtual machine workloads.

The Ceph environment was operated using:

* Ceph monitors
* Ceph OSDs
* Ceph storage pools
* Distributed storage capacity
* Proxmox-to-Ceph integration

The environment was observed in a healthy operational state during validation.

### Verified Ceph Environment

The production environment was observed with:

* Ceph Squid 19.2.6
* 7 OSDs
* Approximately 38.95 TiB of Ceph storage capacity
* VM storage pool used by the Proxmox environment
* Ceph health status reported as healthy during validation

Production storage identifiers and node-specific details are intentionally excluded from this public documentation.

---

## VM Storage and Placement

One important operational consideration was the relationship between:

```text
Proxmox VM
     |
     v
Proxmox Storage Integration
     |
     v
Ceph Distributed Storage
     |
     v
Ceph OSDs
```

VM placement and migration were evaluated with awareness of:

* Available compute resources
* VM resource requirements
* Storage availability
* Ceph health
* Cluster node status
* Workload impact

This approach helps avoid treating virtualization compute and storage as completely independent components.

---

## VM Migration

Hands-on work included moving a production virtual machine between Proxmox cluster nodes.

The migration required consideration of:

1. VM operational state
2. Target node availability
3. Storage accessibility
4. Ceph health
5. Network connectivity
6. VM service availability
7. Post-migration validation

A successful migration requires validation beyond simply confirming that the VM appears on the destination node.

### Post-Migration Validation

Validation included checking:

* VM power state
* VM accessibility
* Network connectivity
* Application/service availability
* Storage availability
* Proxmox cluster health
* Ceph health

---

## Mail Infrastructure Virtualization

A production **Mailcow** virtual machine was operated within the Proxmox environment.

The VM was moved between Proxmox cluster nodes as part of infrastructure management.

The migration demonstrated practical administration of an application workload running on clustered virtualization infrastructure.

The public documentation intentionally excludes:

* Production public IP address
* Production mail domain
* VM ID
* Proxmox node names
* Internal network addressing
* Mail system credentials
* Sensitive mail configuration

The Mail Infrastructure project documents the mail platform itself in greater detail.

---

## Ceph Health Monitoring

Ceph health was monitored as an important dependency of the virtual machine environment.

Operational validation included checking:

* Overall Ceph health
* OSD availability
* Storage pool status
* Cluster state
* Available capacity
* Proxmox storage visibility

A healthy virtualization environment depends not only on the VM state but also on the health of its underlying storage platform.

---

## Troubleshooting Methodology

Troubleshooting was performed using a layered approach.

### Layer 1 — Proxmox Cluster

Check:

* Node availability
* Cluster membership
* Cluster services
* Resource utilization

### Layer 2 — VM

Check:

* VM power state
* CPU and memory allocation
* Virtual hardware
* VM console
* Guest operating system

### Layer 3 — Network

Check:

* Virtual network configuration
* Connectivity
* VLAN configuration
* Physical network path

### Layer 4 — Storage

Check:

* Proxmox storage status
* Ceph health
* OSD availability
* Storage pool status
* VM disk accessibility

### Layer 5 — Application

Check:

* Guest operating system services
* Application services
* Application connectivity
* End-to-end functionality

This layered approach helps determine whether a problem originates from the virtualization platform, guest operating system, network, storage subsystem, or application.

---

## Configuration and Operational Validation

Validation procedures included:

* Proxmox node health checks
* Cluster status verification
* VM state verification
* VM network connectivity testing
* Storage visibility checks
* Ceph health verification
* OSD status validation
* Storage pool validation
* Post-migration service verification

Operational changes were validated after implementation rather than relying solely on configuration state.

---

## Engineering Decisions

### Proxmox + Ceph

Using Proxmox with Ceph provides an integrated virtualization and distributed-storage platform suitable for clustered infrastructure workloads.

### Storage-Aware VM Management

VM placement and migration were treated as infrastructure operations involving both compute and storage dependencies.

### Layered Validation

Changes were validated across:

```text
Cluster
   ↓
Node
   ↓
VM
   ↓
Network
   ↓
Storage
   ↓
Application
```

This reduces the risk of declaring a migration or infrastructure change successful based only on the VM power state.

---

## Lessons Learned

* Virtualization troubleshooting requires understanding the underlying storage architecture.
* A VM can appear healthy while its storage subsystem has problems.
* Ceph health should be checked before and after significant VM operations.
* VM migration requires application-level validation, not only hypervisor validation.
* Distributed storage introduces additional dependencies that must be included in troubleshooting.
* Resource management should consider both compute and storage requirements.
* Documentation should capture operational validation steps as well as configuration.

---

## Security Considerations

The production environment contains sensitive infrastructure information that is intentionally excluded from this public project.

This repository does not contain:

* Production IP addresses
* Internal hostnames
* Production domain names
* VM identifiers
* Storage identifiers
* Credentials
* Authentication keys
* Certificates
* MAC addresses
* Detailed production network topology
* Sensitive cluster configuration
* Backup or recovery credentials

The project describes the engineering work and architecture at a technology level without exposing information that could assist unauthorized access to the production environment.

---

## Technologies

* Proxmox VE
* Ceph
* Ceph Squid
* Distributed storage
* Virtual machines
* Clustered virtualization
* VM migration
* Virtual networking
* Storage pools
* OSD management
* Linux
* Windows Server
* Mailcow
* Enterprise networking

---

## Project Outcome

The Proxmox and Ceph environment provided a clustered virtualization platform with distributed storage for enterprise workloads.

Hands-on administration included:

* Proxmox cluster operations
* VM management
* VM migration
* Ceph storage administration
* Storage health monitoring
* Cluster validation
* Virtual networking
* Infrastructure troubleshooting
* Post-change operational validation

The project demonstrates practical experience operating virtualization infrastructure where **compute, networking, storage, and application availability must be managed as an integrated system**.
