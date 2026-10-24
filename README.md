# Network & Infrastructure Engineering Portfolio

Welcome to my professional technical portfolio.

I am a **Network & Infrastructure Engineer with 18 years of experience** supporting hospital and enterprise IT environments. My experience spans enterprise networking, network security, Windows and Linux infrastructure, virtualization, security monitoring, mail services, and infrastructure troubleshooting.

This repository showcases selected engineering projects, infrastructure implementations, technical investigations, configuration examples, validation procedures, and lessons learned from real-world operational environments.

> **Security Notice:** This public portfolio is sanitized. Credentials, secrets, private keys, certificates, sensitive internal addressing, confidential hostnames and domains, and other restricted operational information are excluded.

---

## Core Technical Areas

### Enterprise Networking

- Cisco enterprise switching and routing
- VLANs and inter-VLAN routing
- Layer 2 and Layer 3 troubleshooting
- HSRP and gateway redundancy
- Spanning Tree Protocol
- EtherChannel and trunking
- Network segmentation and access control
- SPAN and network traffic visibility
- MDF/IDF network architecture

### Network Security

- Cisco ASA firewall infrastructure
- pfSense firewall administration
- Firewall policies and traffic filtering
- DMZ and network segmentation
- VPN infrastructure
- RADIUS-based network authentication
- Intrusion detection and security monitoring

### Monitoring and Security Operations

- Wazuh SIEM
- Suricata IDS
- Windows security event collection
- Network authentication monitoring
- Log analysis and alert investigation
- File integrity and file activity monitoring
- Log retention and storage capacity planning
- Operational validation and troubleshooting

### Windows Infrastructure

- Windows Server administration
- Active Directory
- DNS and DHCP
- Microsoft Network Policy Server (NPS) and RADIUS
- File services and file auditing
- System administration and troubleshooting
- IIS and Windows-based infrastructure services

### Virtualization and Infrastructure

- Microsoft Hyper-V
- Hyper-V Replica
- VMware ESXi
- Proxmox VE
- Ceph storage
- Virtual machine administration
- Infrastructure availability and recovery planning
- Storage capacity and resource management

### Linux and Infrastructure Services

- Ubuntu Server and Debian
- Linux service administration
- Squid proxy infrastructure
- Mail server infrastructure
- Web and application services
- Service monitoring, logging, and troubleshooting

---

## Selected Engineering Projects

The following directories contain project areas for technical documentation and portfolio development.

| **Project**                          | **Focus**                                                           | **Repository**                                                                                                                                  |
| ------------------------------------ | ------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Enterprise Network Infrastructure    | Switching, routing, VLANs, redundancy, and network topology         | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/03-enterprise-network)            |
| Firewall and Security Infrastructure | Firewall administration, DMZ, and security policies                 | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/04-firewall-security)             |
| Suricata IDS                         | Network intrusion detection, traffic visibility, and event analysis | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/01-suricata-ids)                  |
| Wazuh SIEM                           | Centralized security monitoring and event collection                | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/02-wazuh-siem)                    |
| Windows Infrastructure               | Windows Server, NPS/RADIUS, and infrastructure services             | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/05-windows-infrastructure)        |
| File Auditing                        | File activity monitoring and security auditing                      | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/06-file-auditing)                 |
| Hyper-V Infrastructure               | Virtualization and workload administration                          | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/07-hyper-v-infrastructure)        |
| Hyper-V Replica                      | Virtual machine replication and recovery planning                   | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/08-hyper-v-replica)               |
| VMware Infrastructure                | ESXi virtualization and workload administration                     | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/09-vmware-infrastructure)         |
| Linux Services Infrastructure        | Linux systems and infrastructure services                           | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/10-linux-services-infrastructure) |
| Proxmox and Ceph Infrastructure      | Virtualization and storage infrastructure                           | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/11-proxmox-ceph-infrastructure)   |
| Mail Infrastructure                  | Mail services and supporting infrastructure                         | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/12-mail-infrastructure)           |
| Asset Management                     | Infrastructure asset inventory and lifecycle management             | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/13-asset-management)              |
| Proxy Infrastructure                 | Squid proxy deployment, access controls, and logging                | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/14-proxy-infrastructure)          |
| Domain Controller Restoration & Active Directory Recovery | Active Directory recovery, FSMO role management, DNS/DHCP, Windows Server modernization | [View project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/tree/main/projects/15-domain-controller-restoration) |

*These links point to the repository's project directories. The documentation within each directory should be reviewed separately for completeness and publication readiness.*

---

## Featured Engineering Experience

### 1. Hospital Core Network Modernization and Redundancy — 2021

Implemented a core network modernization involving an additional Cisco Catalyst C9407R alongside the existing Catalyst 4506-E core infrastructure, with Catalyst 2960X access switches.

Key areas included:

- Core switching and network redundancy
- HSRP gateway redundancy across VLANs 10–90
- Inter-core trunking and EtherChannel
- Rapid-PVST spanning-tree operation
- Aggregated MDF/IDF connectivity
- Redundancy and failover validation

**Validation:** Core redundancy/failover testing was successfully completed on June 17, 2021.

[View enterprise network project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/03-enterprise-network)

### 2. Network-Wide RADIUS Authentication — 2022

Implemented centralized RADIUS-based authentication for supported network devices using Microsoft Windows Network Policy Server (NPS).

The broader monitoring work subsequently included Wazuh integration in 2026.

Key areas included:

- Centralized network-device authentication
- Microsoft NPS/RADIUS
- Authentication troubleshooting
- Security-event monitoring integration

[View Windows infrastructure project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/05-windows-infrastructure) · [View Wazuh SIEM project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/02-wazuh-siem)

### 3. Windows Server VPN Infrastructure — 2022

Implemented VPN services using Windows Server Routing and Remote Access Service (RRAS).

Subsequent monitoring work included Wazuh integration with the AmeenFS1 environment in 2026.

Key areas included:

- RRAS VPN configuration
- VPN connectivity troubleshooting
- Windows infrastructure administration
- Security monitoring integration

[View Windows infrastructure project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/05-windows-infrastructure)

### 4. Squid Proxy Infrastructure — 2023–2026

Worked on Squid proxy infrastructure, including service configuration, access controls, traffic filtering, and proxy logging.

Subsequent work included integrating proxy log collection with Wazuh in 2026.

Key areas included:

- Squid proxy service administration
- Source-network and VLAN-based access controls
- Destination filtering
- Proxy logging and troubleshooting
- Centralized log collection and monitoring

[View proxy infrastructure project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/14-proxy-infrastructure) · [View Wazuh SIEM project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/02-wazuh-siem)

### 5. IP Address Reconstruction and Network Topology Modernization — 2017

Contributed to IP addressing reconstruction and network topology modernization in an enterprise environment using Cisco Catalyst 4506-E Layer 3 infrastructure.

Key areas included:

- IP addressing and network topology
- VLAN gateways and Layer 3 services
- Access control lists (ACLs)
- DHCP and policy-based routing (PBR)
- Fiber backbone connectivity between MDF and IDFs

Historical reporting dated June 19, 2017, recorded successful 10 Gb fiber testing at five of seven IDFs at that time.

[View enterprise network project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/03-enterprise-network)

---

## Security Monitoring and Infrastructure Projects

### Suricata IDS and Log Retention

A project area covering network intrusion detection and operational log management.

Topics include:

- Network traffic visibility and SPAN
- Suricata event generation and `eve.json` analysis
- Log volume and storage capacity investigation
- Log rotation, compression, and retention
- Configuration validation and operational monitoring

Documentation should distinguish verified implementation details from planned enhancements and examples.

[View Suricata IDS project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/01-suricata-ids)

### Wazuh Security Monitoring

A project area covering centralized security monitoring and integration with infrastructure log sources.

Topics include:

- Agent deployment and management
- Windows security event collection
- File integrity and file activity monitoring
- NPS authentication monitoring
- IDS and proxy telemetry integration
- Security event investigation
- Dashboard use and log-retention considerations

[View Wazuh SIEM project](https://github.com/philipylanan/enterprise-network-infrastructure-portfolio/blob/main/projects/02-wazuh-siem)

---

## Engineering Approach

My engineering approach follows a structured process:

**Understand → Investigate → Design → Validate → Implement → Monitor → Document**

I prioritize:

- Evidence before assumptions
- Controlled and carefully assessed changes
- Configuration and connectivity validation
- Clear rollback considerations
- Post-implementation monitoring
- Capacity and storage planning
- Security-conscious documentation
- Accurate technical records

The objective is not simply to make a system work, but to understand **why it works, how it behaves under load, how it can fail, and how it can be maintained**.

---

## Technical Documentation Standards

Project documentation may include:

- Architecture and topology diagrams
- Sanitized configuration examples
- CLI commands and relevant verified outputs
- Configuration explanations
- Troubleshooting procedures
- Validation and testing procedures
- Capacity planning
- Change-management considerations
- Recovery and rollback procedures
- Operational findings and lessons learned

Technical documentation should clearly distinguish:

- Verified current configuration
- Historical implementation details
- User-reported test results
- Representative commands or examples
- Planned work that has not yet been implemented

All public examples must be reviewed and sanitized before publication. No credentials, private keys, confidential operational information, or unverified technical results should be included.

---

## Technologies

**Networking:** Cisco IOS/IOS-XE, VLANs, STP, HSRP, EtherChannel, routing, SPAN

**Security:** Cisco ASA, pfSense, Suricata IDS, Wazuh SIEM, VPN, firewall policies, IDS/IPS

**Windows:** Windows Server, Active Directory, DNS, DHCP, NPS/RADIUS, IIS, file auditing

**Virtualization:** Hyper-V, Hyper-V Replica, VMware ESXi, Proxmox VE

**Linux and Services:** Ubuntu Server, Debian, Squid, mail infrastructure

**Storage and Operations:** Ceph, RAID, virtualization storage, log retention, capacity planning, monitoring, troubleshooting

---

## Professional Development

My continuing technical development focuses on:

- Enterprise network design methodology and architecture
- Enterprise routing and switching
- Network security and segmentation
- Infrastructure architecture and reliability
- Virtualization and storage
- Security monitoring and log analysis
- Scripting and operational improvements

I continue to strengthen my understanding of enterprise network design principles and structured infrastructure engineering practices.

---

## About This Repository

This portfolio is intended to demonstrate **practical engineering capability**, supported by clear technical reasoning and responsible documentation.

The projects emphasize real-world problem solving, troubleshooting methodology, architecture decisions, technical validation, security considerations, operational reliability, and maintainable infrastructure.

The repository will continue to evolve as additional project documentation, diagrams, and sanitized technical case studies are completed and reviewed.

---

## Contact

**Philip Wenceslao Ylanan**\
Network & Infrastructure Engineer

GitHub: [@philipylanan](https://github.com/philipylanan)
