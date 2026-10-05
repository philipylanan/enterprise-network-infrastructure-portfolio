# Windows Infrastructure

## Project Overview

This project documents the administration, monitoring, troubleshooting, and operational management of Windows Server infrastructure within an enterprise environment.

The Windows infrastructure supported core services including **Active Directory, DNS, DHCP, NPS/RADIUS, file services, auditing, IIS, and application workloads**.

The project demonstrates practical Windows infrastructure engineering across server administration, security monitoring, service validation, troubleshooting, and integration with broader network and security systems.

All environment-specific information has been sanitized for public documentation.

---

## Objectives

* Maintain reliable Windows Server infrastructure.
* Support Active Directory domain services.
* Maintain DNS and DHCP services.
* Provide centralized authentication through NPS/RADIUS.
* Support Windows file-server infrastructure.
* Implement file and security auditing.
* Support IIS-based applications and web services.
* Integrate Windows security telemetry with centralized monitoring.
* Troubleshoot Windows infrastructure and service issues.
* Validate infrastructure changes and service availability.

---

## Windows Server Environment

The environment included multiple Windows Server systems supporting different infrastructure roles.

Examples of workloads included:

* **Active Directory Domain Services**
* **DNS**
* **DHCP**
* **NPS / RADIUS**
* **Windows file services**
* **File auditing**
* **IIS web services**
* **Application servers**
* **Database infrastructure**
* **Hyper-V virtualization hosts**

Different servers were assigned specific infrastructure roles to provide separation of services and operational resilience.

Exact production hostnames, IP addresses, domains, and hardware identifiers are intentionally excluded from this public documentation.

---

## Active Directory

Active Directory provided centralized identity and infrastructure management.

Operational responsibilities included:

* Domain-service administration
* User and computer authentication
* Domain-controller monitoring
* Group Policy integration
* DNS integration
* Security-event monitoring
* Domain-service troubleshooting
* Infrastructure validation

Active Directory infrastructure was also integrated with centralized security monitoring to provide visibility into Windows security events.

---

## DNS Infrastructure

DNS was an essential dependency for the Windows environment.

DNS functionality supported:

* Active Directory name resolution
* Server and client connectivity
* Application services
* Infrastructure service discovery
* Internal hostname resolution

DNS troubleshooting considered:

* Server availability
* Forward lookups
* Reverse lookups where applicable
* DNS configuration
* Client resolver configuration
* Active Directory integration
* Network connectivity

DNS service availability was validated when investigating domain, application, and server connectivity issues.

---

## DHCP Infrastructure

Windows DHCP services provided automated network configuration for applicable client networks.

Operational considerations included:

* DHCP scope management
* Address allocation
* Lease management
* Network options
* DNS server configuration
* Default gateway configuration
* Scope availability
* Client connectivity

DHCP troubleshooting involved validating scope availability, lease allocation, network configuration, and client communication.

---

## NPS / RADIUS

Windows Network Policy Server provided centralized network authentication services for supported access scenarios.

The NPS environment was used for authentication-related services including VPN access.

Security monitoring included Windows NPS authentication events such as:

* **Event ID 6272** — successful network-policy authentication
* **Event ID 6273** — failed network-policy authentication

These events were collected through centralized monitoring to provide visibility into authentication activity.

---

## Windows File Services

Windows file-server infrastructure provided shared storage and file-access services.

Operational responsibilities included:

* File-share administration
* Access-control management
* File-system permissions
* Share permissions
* Storage monitoring
* File auditing
* Security-event monitoring
* Troubleshooting file-access issues

File access and security were considered together to ensure that users could access required resources while unauthorized activity could be detected.

---

## File Auditing

File auditing was implemented to provide visibility into important file-system activity.

The monitoring design incorporated:

* **Windows security auditing**
* **Security audit policy**
* **SACL-based auditing**
* **File creation monitoring**
* **File modification monitoring**
* **File deletion monitoring**
* **Centralized security-event collection**

A PowerShell-based operational mechanism was also used to support file-deletion auditing.

The resulting security telemetry was integrated with Wazuh for centralized investigation.

Production file paths, share names, server names, and organization-specific audit configurations are excluded from this public case study.

---

## IIS Infrastructure

Windows infrastructure also included IIS-based application and web-service workloads.

Operational activities included:

* IIS site administration
* Website bindings
* Application-pool management
* Windows service dependencies
* Application-service troubleshooting
* Network connectivity validation
* DNS and hostname validation
* Application availability checks

IIS troubleshooting considered the complete service path rather than IIS configuration alone.

This included:

```text
Client
  |
  v
DNS
  |
  v
Network Connectivity
  |
  v
Firewall / Security Policy
  |
  v
IIS
  |
  v
Application
  |
  v
Backend Services
```

Production website names, bindings, application details, and internal service information are intentionally excluded.

---

## Hyper-V Infrastructure

Windows Server infrastructure also included Hyper-V virtualization.

Hyper-V was used to host selected infrastructure and application workloads.

Operational considerations included:

* Virtual-machine administration
* Virtual CPU and memory allocation
* Virtual networking
* VLAN configuration
* Virtual switch management
* Storage allocation
* VM connectivity
* Hyper-V Replica
* Guest operating-system troubleshooting

Virtualization was managed as part of the wider infrastructure rather than as an isolated platform.

---

## Hyper-V Replica

Hyper-V Replica was used to provide replication capability for selected virtual-machine workloads.

Operational considerations included:

* Replica configuration
* Primary and replica host roles
* Replication frequency
* Authentication
* Replica health
* Storage requirements
* Network connectivity
* Failover considerations

Replica health was monitored as part of infrastructure operations.

Replication configuration and production host details are excluded from this public documentation.

---

## Windows Security Monitoring

Windows security telemetry was integrated with centralized Wazuh monitoring.

The monitoring architecture included:

```text
Windows Servers
      |
      v
Windows Security Events
      |
      v
Wazuh Agents
      |
      v
Wazuh Manager
      |
      v
Security Dashboards
      |
      v
Event Investigation
```

This provided centralized visibility across multiple Windows infrastructure roles.

---

## Windows Troubleshooting Methodology

Windows infrastructure troubleshooting followed a structured approach.

1. **Identify the affected server or service.**
2. **Determine the expected service behavior.**
3. **Check server and network connectivity.**
4. **Check DNS resolution.**
5. **Check service status.**
6. **Review Windows Event Logs.**
7. **Check authentication and permissions.**
8. **Check firewall and network-policy behavior.**
9. **Review related application or infrastructure dependencies.**
10. **Validate the service after corrective action.**

This approach helped distinguish operating-system, network, authentication, permission, application, and dependency-related issues.

---

## Configuration and Operational Validation

Windows infrastructure changes were validated through configuration and operational checks.

Validation activities included:

* Checking server availability
* Checking Windows services
* Reviewing Event Viewer
* Validating DNS resolution
* Validating DHCP operation
* Checking Active Directory health
* Reviewing NPS authentication events
* Testing file-server access
* Reviewing file-audit events
* Checking IIS application availability
* Checking Hyper-V virtual machines
* Reviewing replica health
* Confirming Wazuh telemetry

The objective was to confirm that changes produced the expected operational result without unintentionally affecting dependent services.

---

## Engineering Decisions

### **Role-Based Infrastructure Design**

Windows servers were used for specific infrastructure and application roles to simplify administration and troubleshooting.

### **Centralized Security Monitoring**

Windows security events were integrated with Wazuh to provide centralized visibility instead of relying exclusively on individual server logs.

### **Layered Validation**

Windows issues were investigated across operating-system, service, network, DNS, authentication, firewall, and application dependencies.

### **Security-Aware File Services**

File-server access and auditing were treated as complementary requirements: users required appropriate access while security monitoring provided visibility into important activity.

### **Virtualization Integration**

Hyper-V was treated as part of the overall infrastructure architecture, including virtual networking, storage, VM administration, and replication.

---

## Lessons Learned

### **1. Windows Services Are Highly Interdependent**

Problems involving Active Directory, DNS, DHCP, authentication, or applications can affect multiple infrastructure components.

### **2. DNS Should Be Checked Early**

Many Windows infrastructure and application problems can appear to be service failures when the underlying issue is name resolution.

### **3. Event Logs Provide Valuable Evidence**

Windows Event Logs provide important information for identifying authentication, service, application, and operating-system problems.

### **4. File Auditing Requires Careful Design**

Auditing must provide useful security visibility without generating unnecessary event volume or excessive storage consumption.

### **5. Virtualization Requires Infrastructure-Level Thinking**

VM performance and availability depend on more than guest configuration. Host resources, storage, virtual networking, and replication must also be considered.

### **6. Changes Must Be Validated End-to-End**

A service being configured correctly does not necessarily mean that the complete application or user workflow is functioning correctly.

---

## Security Considerations

This public case study intentionally excludes:

* Real IP addresses
* Real hostnames
* Real domains
* Public IP assignments
* MAC addresses
* Administrator credentials
* Service-account credentials
* Certificates and private keys
* Production Group Policy details
* Sensitive firewall rules
* Production file paths and shares
* Sensitive application configuration
* Personally identifiable information

The technical concepts and engineering methodology are preserved while production-sensitive information is sanitized.

---

## Technologies

* **Windows Server**
* **Active Directory Domain Services**
* **DNS**
* **DHCP**
* **NPS / RADIUS**
* **Windows File Services**
* **Windows Security Event Logging**
* **File and Security Auditing**
* **PowerShell**
* **IIS**
* **Hyper-V**
* **Hyper-V Replica**
* **Wazuh**
* **Group Policy**
* **Windows infrastructure troubleshooting**

---

## Project Outcome

The Windows infrastructure provided a broad set of enterprise services supporting identity, networking, authentication, file services, applications, virtualization, and security monitoring.

The resulting infrastructure capability included:

* **Active Directory administration**
* **DNS and DHCP services**
* **NPS/RADIUS authentication**
* **Windows file services**
* **File and security auditing**
* **IIS application infrastructure**
* **Hyper-V virtualization**
* **Hyper-V Replica**
* **Centralized Windows security monitoring**
* **Structured troubleshooting and validation**

The project demonstrates practical Windows infrastructure engineering while balancing **availability, security, service dependencies, monitoring, and operational reliability**.
