# Asset Management Infrastructure

## Project Overview

This project documents hands-on deployment and administration of an **IT asset management platform using Snipe-IT** within an enterprise infrastructure environment.

The platform was deployed as a dedicated Linux virtual machine and used to support centralized tracking and management of IT assets, infrastructure equipment, and related inventory information.

Production-specific IP addresses, hostnames, domain names, asset identifiers, user information, credentials, and other sensitive organizational information have been sanitized.

---

## Objectives

* Deploy and administer an IT asset management platform
* Maintain centralized infrastructure asset records
* Support asset inventory and lifecycle management
* Track hardware and infrastructure equipment
* Provide a centralized inventory reference for IT operations
* Maintain accurate asset information
* Support infrastructure documentation and operational planning
* Troubleshoot application and server-side issues
* Validate application availability and network accessibility
* Maintain secure asset-management practices

---

## Asset Management Architecture

The asset-management platform operates as a dedicated Linux virtual machine.

### High-Level Architecture

```text
                    IT Infrastructure
                           |
                           |
                  +-------------------+
                  |   Asset Sources   |
                  +-------------------+
                           |
                           v
                  +-------------------+
                  |     Snipe-IT      |
                  | Asset Management  |
                  +-------------------+
                           |
                    +--------------+
                    | Linux Server |
                    |     VM       |
                    +--------------+
                           |
                    +--------------+
                    | Virtualization|
                    | Infrastructure|
                    +--------------+
```

The architecture is represented conceptually and does not expose production addressing, hostnames, asset identifiers, or organizational information.

---

## Snipe-IT Platform

The environment uses **Snipe-IT** as the centralized IT asset-management platform.

Snipe-IT provides functionality for managing information associated with IT equipment and infrastructure assets.

Operational administration focused on:

* Application availability
* Asset inventory
* Hardware records
* Asset lifecycle information
* Assignment and ownership records
* Infrastructure documentation
* Server and application health
* Network accessibility
* Data accuracy

The public portfolio intentionally excludes actual asset records and organization-specific inventory information.

---

## Linux Virtual Machine

Snipe-IT was deployed on a dedicated **Debian Linux virtual machine**.

The server environment provided:

* Linux operating system
* Virtual CPU and memory resources
* Virtual storage
* Network connectivity
* Application hosting
* Web-based access to the asset-management platform

The application therefore depends on both the Linux operating system and the underlying virtualization infrastructure.

---

## Asset Inventory Management

The platform supports centralized tracking of IT assets across the infrastructure environment.

Asset-management activities can include:

* Hardware inventory
* Server inventory
* Network equipment inventory
* Virtual infrastructure records
* Asset categorization
* Manufacturer information
* Model information
* Serial-number tracking
* Asset status
* Lifecycle information
* Assignment records
* Location information

Production asset records are intentionally not reproduced in this public project.

---

## Asset Lifecycle

Asset management was approached as a lifecycle process rather than simply maintaining a static hardware list.

A typical lifecycle can be represented as:

```text
Procurement
    ↓
Registration
    ↓
Deployment
    ↓
Assignment
    ↓
Operational Use
    ↓
Maintenance
    ↓
Retirement
    ↓
Disposal
```

Maintaining lifecycle information helps infrastructure teams understand the current operational status and history of equipment.

---

## Infrastructure Documentation Integration

Asset management complements technical infrastructure documentation.

The relationship can be represented as:

```text
Infrastructure
      |
      +---- Network Devices
      |
      +---- Servers
      |
      +---- Virtual Machines
      |
      +---- Security Systems
      |
      +---- Storage
      |
      +---- Endpoints
              |
              v
          Snipe-IT
              |
              v
       Central Inventory
```

This provides a centralized reference point that can support infrastructure planning and operational troubleshooting.

---

## Virtual Infrastructure Assets

The asset-management platform was also part of the broader virtualized infrastructure environment.

Virtualization introduces additional inventory considerations, including:

* Physical hosts
* Virtual machines
* Virtual infrastructure services
* Storage infrastructure
* Network connectivity
* Application dependencies

Maintaining accurate records helps distinguish physical infrastructure from the workloads and services operating on it.

---

## Asset Data Quality

Accurate asset management depends on maintaining consistent information.

Important data-quality considerations include:

* Correct asset identification
* Consistent naming
* Accurate hardware information
* Current lifecycle status
* Correct ownership or assignment
* Current location information
* Avoiding duplicate records
* Updating records after infrastructure changes

Asset data should be reviewed and updated when equipment is deployed, moved, reassigned, upgraded, or retired.

---

## Application Availability

Application availability was evaluated across multiple infrastructure layers.

### Application Layer

Check:

* Snipe-IT web interface
* Application availability
* User access
* Asset database functionality

### Operating System Layer

Check:

* Linux server availability
* System resources
* Running services
* Filesystem capacity
* System logs

### Network Layer

Check:

* Network connectivity
* DNS resolution
* Web access
* Firewall path

### Virtualization Layer

Check:

* VM state
* Virtual hardware
* Virtual networking
* Storage availability

This layered approach helps determine whether an asset-management problem originates from the application, operating system, network, or virtualization platform.

---

## Troubleshooting Methodology

Troubleshooting followed a structured, layered process.

### Step 1 — Verify Virtual Machine

Check:

* VM power state
* CPU and memory availability
* Virtual hardware
* Storage availability

### Step 2 — Verify Linux

Check:

* Operating system health
* Running services
* System resources
* Filesystem utilization
* System logs

### Step 3 — Verify Network

Check:

* Network connectivity
* DNS resolution
* Web access
* Firewall path

### Step 4 — Verify Application

Check:

* Snipe-IT service availability
* Web interface
* Application functionality
* Asset database accessibility

### Step 5 — Validate User Access

Check:

* Web application accessibility
* Authentication
* Asset records
* User-facing functionality

This process helps isolate infrastructure problems before making application-level changes.

---

## Configuration and Operational Validation

Operational validation included:

* VM state verification
* Linux system health checks
* Filesystem checks
* Service validation
* Network connectivity testing
* DNS validation
* Web interface accessibility
* Application availability
* Asset-management functionality

Changes were validated after implementation to confirm that the application and supporting infrastructure remained operational.

---

## Security Considerations

Asset-management systems can contain sensitive infrastructure information and therefore require appropriate access control.

This public project does not contain:

* Production IP addresses
* Internal hostnames
* Production domain names
* Asset numbers
* Serial numbers
* MAC addresses
* User information
* Device assignments
* Credentials
* Authentication secrets
* API keys
* Database credentials
* Actual inventory records
* Internal infrastructure identifiers

Asset inventory should be protected because detailed infrastructure records can provide valuable information about an organization's technology environment.

---

## Engineering Decisions

### Centralized Asset Management

Using a dedicated asset-management platform provides a centralized inventory rather than relying on disconnected spreadsheets or manually maintained lists.

### Dedicated Linux Application Server

Running Snipe-IT on a dedicated Linux VM separates the asset-management application from unrelated infrastructure services and provides a manageable application-hosting environment.

### Infrastructure Integration

Asset management was treated as part of the broader infrastructure-management process rather than as an isolated inventory task.

### Lifecycle-Based Management

Assets should be maintained throughout their operational lifecycle so that inventory records remain useful for planning, troubleshooting, maintenance, and retirement activities.

---

## Lessons Learned

* Accurate inventory is an important component of infrastructure management.
* Asset records become more valuable when they are kept current.
* Asset management complements network and server documentation.
* Virtualization introduces additional layers that should be represented in infrastructure inventory.
* Asset-management systems themselves require normal server, network, and application monitoring.
* Inventory information should be protected because it can reveal details about an organization's infrastructure.
* Lifecycle-based tracking provides more operational value than maintaining a static equipment list.

---

## Technologies

* Snipe-IT
* Debian Linux
* Linux server administration
* Virtual machines
* Proxmox VE
* Web applications
* IT asset management
* Infrastructure inventory
* Asset lifecycle management
* Network troubleshooting
* Systems administration

---

## Project Outcome

The Snipe-IT platform provided a centralized asset-management capability within the enterprise infrastructure environment.

Hands-on administration included:

* Snipe-IT deployment and administration
* Linux VM management
* Asset inventory management
* Infrastructure asset tracking
* Lifecycle-oriented inventory practices
* Application availability validation
* Network troubleshooting
* Server-side troubleshooting
* Operational documentation
* Security-conscious inventory management

The project demonstrates practical experience integrating **IT asset management into broader enterprise infrastructure operations**, providing a centralized inventory foundation for network, server, virtualization, and systems administration.
