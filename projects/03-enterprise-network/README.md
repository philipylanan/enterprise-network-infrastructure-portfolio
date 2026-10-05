# Enterprise Network Infrastructure Engineering

## Project Overview

This project documents the engineering, configuration, troubleshooting, and operational management of an enterprise network infrastructure supporting a multi-VLAN environment.

The work covers Layer 2 and Layer 3 network architecture, VLAN segmentation, redundancy, spanning-tree operation, EtherChannel, gateway resiliency, access control, traffic monitoring, and SPAN-based security visibility.

The project demonstrates practical network engineering from investigation and design through implementation, validation, monitoring, and documentation.

All environment-specific information has been sanitized for public documentation.

---

## Objectives

* Maintain reliable enterprise network connectivity.
* Provide Layer 2 and Layer 3 network services.
* Implement VLAN-based network segmentation.
* Provide resilient default gateways using HSRP.
* Maintain stable Layer 2 topology using Spanning Tree Protocol.
* Use EtherChannel for link aggregation and redundancy.
* Apply access-control policies where required.
* Provide network traffic visibility for security monitoring.
* Troubleshoot connectivity and switching issues using structured investigation.
* Validate configuration changes before and after implementation.

---

## Network Architecture

The infrastructure uses a hierarchical enterprise network design with a central Layer 3 switching platform providing routing between VLANs and connectivity to downstream network segments.

The architecture includes:

* Core Layer 3 switching
* Access-layer switching
* VLAN segmentation
* Inter-VLAN routing
* First-hop gateway redundancy
* Spanning Tree Protocol
* EtherChannel
* Network access control
* SPAN traffic monitoring
* Firewall/security integration

A simplified architecture is:

```text
                         Internet / WAN
                              |
                              v
                       Firewall / Security
                              |
                              v
                    Core Layer 3 Switching
                       /              \
                      /                \
                     v                  v
             Access Switching      Server Networks
                  |                     |
                  v                     v
             User Devices          Infrastructure
                  |
                  v
          SPAN / Mirrored Traffic
                  |
                  v
             IDS Monitoring
```

The diagram is intentionally simplified and does not expose production addressing or topology details.

---

## VLAN Segmentation

VLANs were used to separate network functions and control Layer 2 broadcast domains.

The production environment included multiple VLANs supporting different infrastructure and operational requirements.

Examples of logical network roles included:

* User/client networks
* Server networks
* Infrastructure management
* Security monitoring
* Specialized application systems
* Wireless or service networks
* Other operational network segments

Inter-VLAN communication was provided through Layer 3 switching and controlled through routing and security policies.

Production VLAN IDs, addressing, and organization-specific mappings are intentionally excluded from this public documentation.

---

## Layer 3 Routing

The core switching infrastructure provided Layer 3 gateway services for VLANs.

The routing design included:

* Switched Virtual Interfaces (SVIs)
* Inter-VLAN routing
* Default gateway services
* Routing and forwarding between network segments
* Access-control enforcement where required

SVI configuration and routing behavior were validated during troubleshooting and operational changes.

---

## Gateway Redundancy

First-hop gateway redundancy was implemented using Hot Standby Router Protocol (HSRP).

HSRP provided resilient default-gateway services for supported VLANs.

The design allowed a standby Layer 3 device to assume gateway responsibility if the active gateway became unavailable.

Operational validation included checking:

* HSRP state
* Active/standby roles
* Virtual gateway status
* Interface status
* VLAN reachability

Production HSRP group numbers, addresses, priorities, and device-specific values are intentionally excluded.

---

## Spanning Tree Protocol

Spanning Tree Protocol was used to maintain a loop-free Layer 2 topology.

The network design required consideration of:

* Root-bridge placement
* Port roles and states
* Forwarding and blocking behavior
* VLAN-specific topology
* Link redundancy
* Topology changes

STP information was reviewed during troubleshooting to identify potential Layer 2 problems and verify expected topology behavior.

---

## EtherChannel

EtherChannel was used where multiple physical links were combined into logical interfaces.

This provided:

* Increased aggregate bandwidth
* Link redundancy
* Simplified logical topology
* Improved resiliency

Operational validation included checking:

* Port-channel state
* Member interfaces
* Negotiation/protocol status
* Interface consistency
* Link status

The implementation used Cisco switching technology and standard EtherChannel operational procedures.

---

## Access Control

Network access controls were used to restrict traffic between selected network segments where required.

ACL design considerations included:

* Source and destination networks
* Protocol and service requirements
* Direction of traffic
* Security boundaries
* Required application communication

ACL changes were validated to ensure that required services remained reachable while unauthorized traffic was restricted.

Production ACL entries and security-policy details are intentionally omitted.

---

## SPAN and Security Monitoring

A key part of the network architecture was providing mirrored network traffic to security-monitoring infrastructure.

Switched Port Analyzer (SPAN) functionality was used to mirror selected production traffic toward an IDS monitoring system.

The simplified traffic flow was:

```text
Production VLAN Traffic
          |
          v
    Core / Switching
          |
          v
       SPAN Port
          |
          v
       IDS Sensor
          |
          v
   Security Monitoring
```

This allowed network traffic to be inspected without placing the IDS sensor directly inline with production traffic.

The mirrored traffic included multiple production VLANs.

Production interface identifiers and VLAN mappings are intentionally excluded.

---

## Network Troubleshooting Methodology

Network troubleshooting followed an evidence-first approach.

The general workflow was:

1. Define the reported problem.
2. Identify the affected network segment.
3. Verify physical and interface status.
4. Check VLAN membership.
5. Check MAC-address learning.
6. Review Spanning Tree state.
7. Check EtherChannel status where applicable.
8. Verify Layer 3 SVI and gateway state.
9. Check routing and ACL behavior.
10. Test connectivity.
11. Review monitoring and logs.
12. Implement the required corrective action.
13. Validate the result.

This approach helps isolate faults systematically rather than making configuration changes based on assumptions.

---

## Configuration Validation

Network configuration changes were validated before and after implementation.

Typical validation activities included:

* Interface status
* VLAN status
* MAC-address learning
* Spanning Tree state
* EtherChannel state
* HSRP state
* SVI status
* Routing behavior
* ACL behavior
* Connectivity testing
* SPAN operation

The exact production command outputs are maintained separately from this public portfolio to avoid exposing sensitive infrastructure information.

---

## Operational Monitoring

The network infrastructure was monitored through a combination of device-level operational checks and centralized security monitoring.

Monitoring activities included:

* Interface health
* Link state
* VLAN availability
* Gateway status
* STP topology
* EtherChannel state
* Routing behavior
* Security events
* IDS telemetry
* Infrastructure logs

This provided visibility into both network availability and security-related activity.

---

## Engineering Decisions

### Layer 3 core

Layer 3 switching at the core provided efficient inter-VLAN routing and centralized gateway services.

### VLAN segmentation

Network segmentation reduced unnecessary Layer 2 adjacency and provided logical separation between operational network functions.

### HSRP

Gateway redundancy reduced the impact of a single Layer 3 gateway failure.

### Spanning Tree

STP provided protection against Layer 2 loops while allowing redundant physical connectivity.

### EtherChannel

Link aggregation provided additional bandwidth and resiliency while presenting a logical interface to the network.

### SPAN-based IDS visibility

Mirrored traffic allowed security monitoring without introducing an inline inspection point into the production forwarding path.

---

## Lessons Learned

### 1. Network troubleshooting should begin with evidence

Interface state, VLAN membership, MAC learning, STP, routing, and ACL behavior should be verified before making changes.

### 2. Redundancy requires operational validation

Having redundant links or gateways is not enough. Their actual operational state must be checked.

### 3. Layer 2 and Layer 3 troubleshooting must be connected

Many connectivity problems cross the boundary between switching and routing. Troubleshooting should follow the packet path.

### 4. Security visibility should be considered during network design

SPAN and IDS integration can provide valuable visibility without requiring the production network to operate through an inline security sensor.

### 5. Documentation is part of network engineering

Accurate records of topology, configuration, validation, and operational behavior make future troubleshooting and change management more reliable.

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
* Production ACL rules
* Exact VLAN-to-network mappings
* Sensitive topology details
* Organization-specific security policies

The technical concepts and engineering methodology are preserved while environment-specific information is sanitized.

---

## Technologies

* Cisco enterprise switching
* Layer 2 switching
* Layer 3 switching
* VLANs
* Inter-VLAN routing
* HSRP
* Spanning Tree Protocol
* EtherChannel
* ACLs
* SPAN
* IDS integration
* Network troubleshooting
* Network monitoring
* Security monitoring

---

## Project Outcome

The enterprise network infrastructure provided a structured and resilient foundation for multiple network and infrastructure services.

The engineering work demonstrated practical capability in:

* Enterprise Layer 2 and Layer 3 networking
* VLAN segmentation
* Gateway redundancy
* STP operation
* EtherChannel
* Network access control
* SPAN-based traffic visibility
* Network troubleshooting
* Configuration validation
* Security-monitoring integration
* Operational documentation

The project demonstrates an evidence-driven approach to maintaining reliable enterprise network infrastructure while incorporating security visibility and operational resilience into the network design.
