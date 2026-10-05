# Linux Services & Infrastructure

## Project Overview

This project documents hands-on administration, configuration, monitoring, storage management, and troubleshooting of Linux-based infrastructure supporting enterprise services.

The Linux environment includes Ubuntu and Debian systems used for security monitoring, network services, application infrastructure, asset management, and supporting services.

The project demonstrates practical experience with:

* Linux server administration
* Ubuntu and Debian
* Service management
* Network configuration and troubleshooting
* Filesystem and storage management
* Log management
* Security monitoring infrastructure
* Proxy services
* Application infrastructure
* System validation
* Operational troubleshooting

---

## Objectives

The primary objectives were to:

* Maintain reliable Linux-based infrastructure
* Deploy and administer required Linux services
* Manage system storage and filesystems
* Monitor service and system health
* Troubleshoot Linux service issues
* Support enterprise network and security infrastructure
* Maintain appropriate log retention
* Validate service availability and operational behavior
* Document Linux infrastructure and operational procedures

---

## Linux Platforms

The environment includes:

* Ubuntu Server
* Debian
* Linux-based virtual machines
* Enterprise network and security services

Linux systems were deployed according to the requirements of the individual service or workload.

---

## Linux Infrastructure Architecture

A simplified representation is:

```text
                    Enterprise Network
                           |
              ---------------------------
              |            |             |
           Security      Network       Application
           Services      Services       Services
              |            |             |
           Linux VM      Linux VM      Linux VM
              |
       -------------------
       |        |        |
      Logs    Storage   Services
```

Linux systems provide supporting services while integrating with the broader Windows, network, virtualization, and security infrastructure.

---

## Security Monitoring Infrastructure

Linux was used as a platform for security monitoring services.

The environment included a Wazuh Manager running on Ubuntu Server and a Suricata IDS system running on Linux.

These systems supported:

* Security event collection
* Log processing
* IDS telemetry
* Alert monitoring
* Network traffic analysis
* Log retention
* Security investigation

The Linux systems were integrated with other infrastructure rather than operating as isolated services.

---

## Suricata Linux Infrastructure

A Linux-based Suricata server was used to inspect mirrored network traffic.

The implementation included:

* Suricata IDS
* Network interface configuration
* SPAN/mirrored traffic processing
* EVE JSON logging
* Alert monitoring
* Log rotation
* Dedicated log storage
* Storage utilization monitoring

Storage management became an important operational requirement because high-volume IDS logging can consume significant disk capacity.

The logging architecture was subsequently optimized to improve retention management and storage utilization.

---

## Wazuh Linux Infrastructure

A Linux-based Wazuh Manager was used for centralized security monitoring.

The implementation included:

* Wazuh Manager
* Agent management
* Security event collection
* JSON log processing
* File auditing integration
* Windows event monitoring
* Network security telemetry
* Security alert investigation

Linux administration was therefore an important component of the organization's security monitoring platform.

---

## Storage and Filesystem Management

Linux storage administration included:

* Filesystem management
* Mount points
* Disk utilization monitoring
* Log storage management
* Storage expansion
* Capacity planning
* Retention management

A dedicated storage volume was added for high-volume Suricata logging.

The storage was formatted with a Linux filesystem and mounted specifically for Suricata log storage.

Operational validation included checking:

* Filesystem capacity
* Mount status
* Available space
* Log growth
* Service operation after storage changes

---

## Log Management and Retention

Log management was an important part of the Linux infrastructure.

The environment required retention planning for services generating significant amounts of telemetry.

Operational activities included:

* Log rotation
* Compression
* Retention periods
* Automated deletion of expired logs
* Storage monitoring
* Log growth analysis

Retention settings were evaluated against:

* Available storage
* Log generation rate
* Security monitoring requirements
* Operational requirements
* Recovery and investigation needs

This demonstrated the importance of balancing retention requirements with actual storage consumption.

---

## Proxy Infrastructure

A Linux server was used to provide proxy services for enterprise network clients.

The proxy environment included:

* Linux server administration
* Squid proxy
* Network access control
* Service management
* Connectivity troubleshooting
* Log monitoring
* Operational validation

The proxy service formed part of the broader network infrastructure and required coordination with network policies and client connectivity.

---

## Application and Infrastructure Services

Linux was also used for application and infrastructure workloads.

Examples include:

* Asset management infrastructure
* Network boot/PXE infrastructure
* Web/application services
* Supporting enterprise services

These systems required standard Linux administration activities including:

* Service monitoring
* Network configuration
* Storage management
* Log review
* Connectivity testing
* System troubleshooting

---

## Linux Service Management

Linux services were managed using standard system administration practices.

Operational checks included:

* Service status
* Process state
* Listening ports
* Network connectivity
* Configuration files
* System logs
* Resource utilization
* Filesystem capacity

Troubleshooting focused on identifying whether a service issue originated from:

* Service configuration
* Operating system state
* Storage
* Network connectivity
* Permissions
* Resource availability
* Upstream infrastructure

---

## Network Troubleshooting

Linux network troubleshooting was performed as part of service administration.

The troubleshooting process considered:

```text
Linux Service
     |
     +---- Process / Service
     |
     +---- Local Configuration
     |
     +---- Network Interface
     |
     +---- Routing
     |
     +---- DNS
     |
     +---- Firewall
     |
     +---- Upstream Network
```

Validation included checking local system state before moving outward toward network infrastructure.

This approach helped distinguish Linux service problems from wider network connectivity issues.

---

## System Validation

Operational validation included:

* Checking service status
* Checking network interfaces
* Checking IP configuration
* Checking routes
* Checking DNS behavior
* Checking listening services
* Checking filesystem capacity
* Reviewing system logs
* Monitoring resource utilization
* Testing service connectivity

Changes were validated after implementation to confirm that services continued operating as expected.

---

## Troubleshooting Methodology

Linux troubleshooting followed an evidence-based approach.

### 1. Service

Check:

* Service status
* Process state
* Configuration
* Service logs

### 2. Operating System

Check:

* CPU
* Memory
* Filesystem
* Permissions
* System logs

### 3. Network

Check:

* Network interface
* IP configuration
* Routing
* DNS
* Connectivity
* Firewall

### 4. Storage

Check:

* Filesystem usage
* Mount status
* Available capacity
* Log growth
* Storage health

### 5. Application

Check:

* Application logs
* Listening ports
* Dependencies
* Connectivity
* Application behavior

This layered methodology reduces unnecessary changes and helps identify the actual source of a problem.

---

## Engineering Decisions

### Service-Specific Linux Deployment

Linux systems were used where the platform was appropriate for the required service.

### Storage-Aware Logging

High-volume security logging was treated as a storage-planning problem rather than simply allowing logs to grow indefinitely.

### Automated Retention

Log rotation and retention mechanisms were used to prevent uncontrolled storage growth.

### Evidence-Based Troubleshooting

Linux service issues were investigated through system state, logs, storage, networking, and application behavior before changes were made.

### Integration with Enterprise Infrastructure

Linux services were designed to operate alongside Windows, network, firewall, virtualization, and security infrastructure.

### Validation After Changes

Service and system behavior were checked after configuration or infrastructure changes.

---

## Lessons Learned

Key lessons from the Linux infrastructure include:

* Linux administration is closely connected to networking and storage management.
* Service availability depends on more than the application process itself.
* High-volume logging requires deliberate storage planning.
* Log rotation and retention should be validated rather than assumed to work.
* Filesystem capacity should be monitored continuously on logging systems.
* Network troubleshooting should begin with local system evidence before moving to upstream infrastructure.
* Linux services can be effectively integrated into predominantly Windows enterprise environments.
* Operational documentation is important for maintaining reliable Linux infrastructure.

---

## Security Considerations

The public version of this project intentionally excludes:

* Production IP addresses
* Production hostnames
* Internal domain names
* Credentials
* API keys
* SSH keys
* Certificates
* MAC addresses
* Exact firewall rules
* Sensitive network topology
* Internal paths containing organization-specific information
* Service credentials
* Organization-specific operational information

The documentation focuses on Linux engineering practices and service administration rather than exposing production infrastructure.

---

## Technologies

* Ubuntu Server
* Debian
* Linux
* Suricata
* Wazuh
* Squid
* Snipe-IT
* PXE
* Linux filesystems
* Logrotate
* systemd
* TCP/IP
* DNS
* Network troubleshooting
* Security monitoring
* Enterprise virtualization

---

## Project Outcome

The Linux infrastructure supports multiple enterprise functions including:

* Security monitoring
* Intrusion detection
* Centralized security event management
* Network proxy services
* Asset management
* Network boot infrastructure
* Application and infrastructure services
* Log management
* Storage management

The project demonstrates practical experience administering Linux systems within an enterprise environment, with emphasis on **service management, networking, storage, logging, troubleshooting, security monitoring, and operational reliability**.
