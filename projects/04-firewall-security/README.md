# Firewall and Security Infrastructure

## Project Overview

This project documents the design, administration, troubleshooting, and operational management of firewall and network-security infrastructure within an enterprise environment.

The environment included multiple firewall platforms supporting perimeter security, DMZ connectivity, internal network protection, VPN services, traffic filtering, network segmentation, and security monitoring.

The project demonstrates practical firewall administration across both commercial and open-source platforms while maintaining separation between production infrastructure and public documentation.

All environment-specific information has been sanitized for public documentation.

---

## Objectives

* Maintain secure connectivity between external, internal, and DMZ network segments.
* Configure and manage firewall interfaces and security zones.
* Apply traffic-filtering and access-control policies.
* Support secure network segmentation.
* Manage firewall-based VPN functionality.
* Integrate firewall traffic with security monitoring.
* Troubleshoot connectivity and security-policy issues.
* Validate firewall configuration changes.
* Maintain operational visibility of security infrastructure.

---

## Firewall Platforms

The environment included two primary firewall platforms.

### **Cisco ASA**

A Cisco ASA firewall provided perimeter-security and network-segmentation functions.

The platform supported:

* **Outside connectivity**
* **Inside network connectivity**
* **DMZ connectivity**
* **Access-control policies**
* **Network address translation**
* **VPN functionality**
* **Security-policy enforcement**
* **Operational troubleshooting**

The ASA configuration was validated using CLI and operational status commands.

### **pfSense**

A pfSense firewall provided additional security and network-management capabilities.

The implementation included:

* **WAN connectivity**
* **LAN/internal connectivity**
* **DMZ connectivity**
* **Firewall rules**
* **NAT**
* **VPN functionality**
* **pfBlockerNG**
* **Suricata IDS/IPS**
* **Traffic management**
* **Network segmentation**

The platform was used where an open-source firewall solution provided an appropriate combination of security capability, flexibility, and operational control.

---

## Network Segmentation

Firewall architecture was used to separate different security zones and network functions.

A simplified architecture can be represented as:

```text
                 Internet / External Network
                            |
                            v
                    +---------------+
                    | Perimeter FW  |
                    +---------------+
                       /           \
                      /             \
                     v               v
              Internal Network     DMZ
                     |
                     v
              Security Monitoring
```

The actual production topology contained additional network segments and infrastructure components that are intentionally excluded from this public documentation.

---

## Access Control and Traffic Filtering

Firewall policies were used to control traffic between security zones.

Policy considerations included:

* Source network
* Destination network
* Protocol
* Destination service/port
* Security-zone boundaries
* Required application connectivity
* Administrative access
* Monitoring requirements

Firewall rules were evaluated according to required business and infrastructure communication rather than allowing unrestricted connectivity.

---

## NAT and Public Services

Network address translation was used to support communication between private infrastructure and externally reachable services where required.

NAT design considerations included:

* Public-to-private service mappings
* Outbound internet access
* DMZ services
* Firewall security policies
* Service exposure
* Address management

Public addresses, internal addresses, service names, and production mappings are intentionally excluded from the public case study.

---

## DMZ Security

DMZ segmentation was used for services requiring controlled communication between external and internal security zones.

The firewall provided policy enforcement between:

```text
External Network
       |
       v
     DMZ
       |
       v
Internal Network
```

Traffic between zones was controlled through explicit firewall policies rather than unrestricted routing.

---

## VPN Infrastructure

VPN functionality was part of the firewall environment.

The implementation included operational management and troubleshooting of VPN services.

VPN validation included checking:

* VPN session status
* IKE security associations
* Tunnel state
* Authentication status
* Connectivity
* Related firewall policies

During one operational validation, the site-to-site VPN service was intentionally stopped.

The firewall was subsequently checked to confirm that there were no active VPN sessions or IKE security associations.

Sensitive VPN configuration, peer addresses, credentials, and cryptographic parameters are excluded from this public documentation.

---

## Security Monitoring Integration

Firewall and network-security infrastructure was integrated with centralized security monitoring where appropriate.

A simplified monitoring workflow was:

```text
Network Traffic
      |
      v
Firewall / Network Infrastructure
      |
      +------------------+
      |                  |
      v                  v
Security Events      SPAN Traffic
                         |
                         v
                    Suricata IDS
                         |
                         v
                    Wazuh SIEM
```

This architecture provided multiple visibility points for investigating network-security events.

---

## Suricata Integration

Suricata was used as an IDS/IPS component within the broader security architecture.

Traffic from selected network segments could be mirrored toward the Suricata monitoring infrastructure for inspection.

This provided additional visibility beyond traditional firewall policy enforcement.

The Suricata implementation and log-retention engineering are documented separately in the **Suricata IDS and Log Retention** project.

---

## pfBlockerNG and Threat Filtering

The pfSense environment included pfBlockerNG for additional network-security filtering.

The implementation provided an additional security-control layer alongside traditional firewall rules.

Threat-filtering functionality was considered together with:

* Firewall policies
* Network segmentation
* IDS/IPS monitoring
* DNS-based filtering
* Operational requirements
* False-positive considerations

Security controls were treated as complementary layers rather than relying on a single protection mechanism.

---

## Traffic Management

Traffic-management functions were also implemented where required.

The pfSense environment included quality-of-service controls for selected network traffic.

Traffic-management design considered:

* Available bandwidth
* Network segments
* Client requirements
* Application requirements
* Security traffic
* Operational priorities

The objective was to provide predictable network behavior while maintaining required security controls.

---

## Firewall Troubleshooting Methodology

Firewall troubleshooting followed a structured approach.

1. **Identify the affected source and destination.**
2. **Determine the expected traffic flow.**
3. **Check interface status.**
4. **Check routing.**
5. **Check NAT behavior.**
6. **Check firewall policy.**
7. **Check VPN state when applicable.**
8. **Capture or inspect traffic where required.**
9. **Review logs and security events.**
10. **Validate the result after changes.**

This approach helped separate routing, NAT, policy, VPN, and application-level problems instead of treating every connectivity issue as a firewall-rule problem.

---

## Configuration Validation

Firewall changes were validated using both configuration and operational checks.

Validation activities included:

* Reviewing interface configuration
* Reviewing firewall policies
* Checking routing
* Checking NAT configuration
* Checking VPN status
* Checking active sessions
* Reviewing logs
* Performing connectivity tests
* Inspecting packet behavior where required
* Confirming expected security-monitoring visibility

For Cisco ASA infrastructure, CLI operational commands were used to verify firewall and VPN state.

For pfSense, configuration and operational status were reviewed through the firewall management interface and supporting diagnostic tools.

---

## Engineering Decisions

### **Layered Security Architecture**

Firewall controls were combined with IDS/IPS, network segmentation, filtering, and centralized security monitoring.

### **Platform Selection**

Different firewall platforms were used according to operational requirements, available resources, security functionality, and infrastructure needs.

### **Explicit Security Policies**

Traffic between security zones was controlled through defined policies rather than unrestricted communication.

### **Security Monitoring Integration**

Firewall infrastructure was considered part of the wider security-monitoring architecture rather than an isolated component.

### **Evidence-Based Troubleshooting**

Connectivity and security issues were investigated using interface state, routing, NAT, policy, session state, packet behavior, and logs.

---

## Lessons Learned

### **1. Firewall Troubleshooting Requires End-to-End Visibility**

A firewall may be functioning correctly while the actual problem exists in routing, NAT, the application, or the destination system.

### **2. Security Policies Should Match Actual Requirements**

Overly broad rules increase exposure, while unnecessarily restrictive rules can disrupt legitimate services. Policies should be based on required communication flows.

### **3. Multiple Security Layers Improve Visibility**

Firewall enforcement, IDS/IPS, filtering, and centralized monitoring provide different security perspectives and work best as complementary controls.

### **4. VPN Status Must Be Verified Operationally**

Configuration alone does not prove that a VPN tunnel is active. Session and IKE state should be checked directly.

### **5. Every Security Change Requires Validation**

Firewall changes should be followed by connectivity, policy, logging, and monitoring validation.

---

## Security Considerations

This public case study intentionally excludes:

* Real IP addresses
* Real hostnames
* Real domains
* Public IP assignments
* MAC addresses
* Firewall credentials
* VPN credentials
* Pre-shared keys
* Cryptographic parameters
* Security-policy details
* Production ACL entries
* Sensitive logs
* Organization-specific topology

The technical architecture and engineering methodology are preserved while production-sensitive information is sanitized.

---

## Technologies

* **Cisco ASA**
* **pfSense CE**
* **Firewall policy management**
* **NAT**
* **DMZ segmentation**
* **VPN**
* **IPsec**
* **pfBlockerNG**
* **Suricata IDS/IPS**
* **Traffic filtering**
* **Quality of Service**
* **Packet analysis**
* **Wazuh SIEM**
* **Network security monitoring**

---

## Project Outcome

The firewall and security infrastructure provided layered network-security controls across perimeter, internal, and DMZ environments.

The resulting architecture provided:

* **Firewall-based traffic enforcement**
* **Network segmentation**
* **DMZ security**
* **NAT and controlled service exposure**
* **VPN operational management**
* **Threat and traffic filtering**
* **IDS/IPS integration**
* **Centralized security monitoring**
* **Structured firewall troubleshooting**
* **Operational configuration validation**

The project demonstrates practical enterprise firewall administration and security engineering while balancing **security, connectivity, visibility, reliability, and operational requirements**.
