# Mail Infrastructure

## Project Overview

This project documents hands-on administration and operational management of a **Mailcow-based mail infrastructure** running as a virtual machine within a Proxmox VE virtualization environment.

The work involved managing the mail platform as an enterprise infrastructure service, including virtualization placement, service availability, public-facing mail infrastructure considerations, webmail administration, migration activities, troubleshooting, and post-change validation.

Production-specific IP addresses, domain names, VM identifiers, Proxmox node names, credentials, certificates, and other sensitive operational information have been sanitized.

---

## Objectives

* Operate and maintain a Mailcow-based mail platform
* Manage the mail server as a virtualized infrastructure workload
* Perform VM placement and migration within Proxmox
* Maintain mail service availability
* Validate mail-related services after infrastructure changes
* Support webmail functionality
* Troubleshoot mail infrastructure issues
* Consider DNS and public service dependencies
* Validate service availability after changes
* Maintain secure operational documentation

---

## Mail Infrastructure Architecture

The mail platform operates as a virtual machine within the Proxmox virtualization environment.

### High-Level Architecture

```text
                         Internet
                            |
                            |
                    Public Mail Services
                            |
                            v
                    +---------------+
                    |  Mail Platform |
                    |    Mailcow     |
                    +---------------+
                            |
                    +---------------+
                    |  Virtual Machine|
                    +---------------+
                            |
                    +---------------+
                    |   Proxmox VE   |
                    +---------------+
                            |
                    +---------------+
                    | Cluster Storage|
                    |     / Ceph     |
                    +---------------+
```

The diagram represents the service architecture conceptually and does not expose production addressing, domain names, VM identifiers, or infrastructure node names.

---

## Mailcow Platform

The environment uses **Mailcow** as the mail platform.

Mailcow provides an integrated mail-service environment containing multiple components required for enterprise email operations.

Operational administration focused on:

* Mail platform availability
* Service status
* Web-based administration
* Webmail availability
* Virtual machine health
* Network connectivity
* DNS dependencies
* Public service accessibility
* Post-change validation

The public portfolio intentionally avoids exposing the organization's actual mail domain and public addressing.

---

## Virtualization Infrastructure

The Mailcow platform runs as a virtual machine on **Proxmox VE**.

This provides the mail platform with:

* Virtual CPU resources
* Virtual memory
* Virtual storage
* Virtual networking
* Proxmox VM lifecycle management
* Cluster-based VM placement
* Access to the underlying distributed storage environment

The Mailcow workload therefore depends on multiple infrastructure layers:

```text
Mail Application
       ↓
Guest Operating System
       ↓
Virtual Machine
       ↓
Proxmox VE
       ↓
Ceph Storage
       ↓
Physical Infrastructure
```

Troubleshooting must consider these layers when investigating service availability issues.

---

## VM Placement and Migration

A production Mailcow virtual machine was moved between Proxmox cluster nodes as part of infrastructure management.

The migration was performed as a virtualization infrastructure operation rather than as a change to the mail application itself.

### Migration Considerations

The migration required consideration of:

1. Source VM state
2. Destination node availability
3. Storage accessibility
4. Ceph health
5. Virtual networking
6. Mail service availability
7. Application accessibility
8. Post-migration validation

### Post-Migration Validation

After the infrastructure operation, validation focused on:

* VM operational state
* Network connectivity
* Storage accessibility
* Mail platform availability
* Web interface accessibility
* Service functionality
* Proxmox cluster health
* Ceph storage health

This ensured that a successful VM migration was not assumed solely from the hypervisor status.

---

## Public Mail Service Considerations

A production mail platform requires several external dependencies to operate correctly.

These include:

* Public DNS
* Mail-related DNS records
* Public network reachability
* SMTP connectivity
* Secure mail protocols
* Webmail access
* TLS certificates
* Firewall/NAT policy
* Service availability

The public portfolio describes these dependencies conceptually without exposing the organization's actual DNS records, public IP addresses, or security policies.

---

## DNS Dependencies

Mail infrastructure relies heavily on correct DNS configuration.

Operational considerations include:

* Mail domain resolution
* MX records
* Hostname resolution
* Mail server addressing
* Reverse DNS considerations
* Authentication-related DNS records
* Email security records

Depending on the deployment, mail authentication and anti-spoofing controls may include:

* SPF
* DKIM
* DMARC

These records are important components of reliable email delivery and sender validation.

---

## Webmail and SOGo

The Mailcow deployment includes **SOGo** as the webmail and groupware interface.

Operational administration included validating webmail availability and ensuring that the user-facing interface remained accessible following infrastructure changes.

The deployed environment also included organization-specific branding within the SOGo interface.

Production branding assets and organization-specific configuration are not reproduced in this public repository.

---

## Mail Service Availability

Mail infrastructure availability was evaluated across multiple layers.

### Infrastructure Layer

* Proxmox VM state
* Host/node availability
* Storage availability
* Ceph health

### Network Layer

* Virtual networking
* Firewall connectivity
* Public reachability
* DNS resolution

### Application Layer

* Mail platform availability
* Webmail accessibility
* Mail service operation
* User-facing functionality

This layered validation approach helps isolate whether an issue originates from the virtualization platform, network, or mail application.

---

## Troubleshooting Methodology

Mail infrastructure troubleshooting followed a structured approach.

### Step 1 — Verify VM

Check:

* VM power state
* CPU and memory availability
* Virtual hardware
* Guest operating system accessibility

### Step 2 — Verify Network

Check:

* Virtual network connectivity
* DNS resolution
* Firewall path
* Public service reachability

### Step 3 — Verify Storage

Check:

* Proxmox storage status
* Ceph health
* VM disk accessibility
* Available capacity

### Step 4 — Verify Mail Platform

Check:

* Mailcow service availability
* Mail-related services
* Web interface
* SOGo accessibility

### Step 5 — Validate End-to-End Service

Check:

* DNS resolution
* Webmail access
* Mail connectivity
* User-facing functionality

This approach prevents application troubleshooting from overlooking an underlying virtualization, storage, or networking problem.

---

## Configuration and Operational Validation

Operational validation included:

* VM state verification
* Proxmox node health checks
* Ceph health verification
* Storage accessibility checks
* Network connectivity testing
* DNS validation
* Mail platform availability checks
* Webmail accessibility testing
* Post-migration service validation

Changes were validated at both the infrastructure and application layers.

---

## Engineering Decisions

### Virtualized Mail Infrastructure

Running the mail platform as a virtual machine provides integration with the existing virtualization environment and allows the workload to be managed using standard Proxmox VM operations.

### Storage-Aware Operations

Because the Mailcow VM depends on distributed storage, VM migration and infrastructure maintenance were performed with awareness of Ceph health and storage availability.

### Layered Troubleshooting

Mail service issues were approached from the infrastructure layer upward:

```text
Physical Infrastructure
        ↓
Ceph Storage
        ↓
Proxmox
        ↓
Virtual Machine
        ↓
Network
        ↓
Mailcow
        ↓
Webmail / Mail Services
```

This provides a repeatable method for identifying the actual failure domain.

---

## Lessons Learned

* Mail infrastructure depends on more than the mail application itself.
* DNS and network reachability are critical dependencies for public mail services.
* VM migrations require application-level validation.
* Distributed storage health should be checked before significant VM operations.
* Webmail availability provides an important user-facing validation point.
* Infrastructure changes should be validated from the hypervisor through to the application.
* Mail service troubleshooting benefits from a layered infrastructure approach.
* Public documentation should describe the architecture without exposing production mail identifiers.

---

## Security Considerations

Mail infrastructure is a high-value service and requires careful handling of sensitive configuration.

This public project does not contain:

* Production public IP addresses
* Production mail domain
* Internal hostnames
* VM identifiers
* Proxmox node names
* Credentials
* Authentication secrets
* Private keys
* TLS certificates
* Actual DNS records
* Firewall rules
* NAT rules
* Mailbox information
* User information
* Organization-specific security configuration

The documentation focuses on engineering practices and infrastructure architecture rather than exposing operational details that could assist unauthorized access.

---

## Technologies

* Mailcow
* SOGo
* Proxmox VE
* Ceph
* Virtual machines
* Linux
* SMTP
* DNS
* TLS
* Webmail
* Enterprise networking
* Firewall infrastructure
* Virtualization
* Distributed storage

---

## Project Outcome

The Mailcow platform was operated as a virtualized enterprise mail workload within the Proxmox environment.

Hands-on administration included:

* Mailcow infrastructure management
* VM administration
* VM migration
* Proxmox integration
* Ceph storage awareness
* Network and DNS validation
* Webmail/SOGo administration
* Service availability validation
* Infrastructure troubleshooting
* Post-change operational verification

The project demonstrates practical experience managing a mail platform as part of a broader **virtualized enterprise infrastructure**, where application availability depends on the coordinated operation of compute, storage, networking, DNS, security, and mail services.
