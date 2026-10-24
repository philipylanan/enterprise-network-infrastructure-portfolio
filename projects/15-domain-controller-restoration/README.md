# Domain Controller Restoration & Active Directory Recovery

**Project period:** August 2023 – July 2025  
**Environment:** Hospital IT infrastructure  
**Focus:** Active Directory recovery, FSMO role management, DNS/DHCP, and Windows Server modernization

## 1. Project Overview

This case study documents the recovery and subsequent modernization of an Active Directory environment following a storage-related failure affecting a Windows Server 2016 domain controller in August 2023.

The recovery relied on a surviving legacy domain controller running Windows Server 2008. Reported recovery actions included Active Directory metadata cleanup, FSMO role seizure when normal transfer was unavailable, and adjustment of Cisco core-switch DHCP relay configuration to address DHCP connectivity for affected clients.

During subsequent infrastructure modernization in 2025, a Windows Server 2016 domain controller was established, FSMO roles were transitioned as part of the modernization sequence, and the existing physical server was rebuilt with Windows Server 2019 Standard as a replacement domain controller. All five FSMO roles were subsequently transferred to the replacement domain controller.

This case study documents the reported implementation sequence, service-role distribution, and representative verification procedures. It distinguishes reported historical actions from verification evidence that is not available in this document.

## 2. Environment and Architecture

The infrastructure involved the following server roles and components across the incident and subsequent modernization:

- **Windows Server 2008 Standard:** Legacy domain controller used during the August 2023 recovery.
- **Windows Server 2016 Standard:** Domain controller established during the modernization sequence, with AD DS and DNS responsibilities; DHCP remained on this server in the later documented baseline.
- **Windows Server 2019 Standard:** Replacement domain controller installed on the existing physical server during the 2025 modernization.
- **Cisco core switching:** DHCP relay configuration associated with the affected VLAN.
- **Windows Server Backup:** Used in the reported legacy-server backup and modernization sequence.

The list describes components involved across the project period; it does not imply that all listed servers operated simultaneously or held identical roles throughout the entire period.

Internal hostnames, IP addresses, domain identifiers, and backup-server names are intentionally omitted from this public case study.

## 3. August 2023 — Incident and Recovery

### Incident

A storage-related failure affected a Windows Server 2016 domain controller and disrupted dependent infrastructure services.

A surviving legacy Windows Server 2008 domain controller provided the recovery path for Active Directory operations.

### Reported recovery actions

1. Assessed the failed domain controller and identified the surviving domain controller available for recovery.
2. Performed Active Directory metadata cleanup for the failed domain controller.
3. Seized FSMO roles to the surviving domain controller because normal transfer was unavailable.
4. Adjusted Cisco core-switch DHCP relay configuration for the affected VLAN.
5. Addressed the reported DHCP connectivity impact for affected clients.

### Technical considerations

Active Directory metadata cleanup and FSMO role seizure are consequential recovery operations. They require assessment of the failed domain controller, the replication state, and the risk of the original server returning to service.

FSMO role seizure differs from normal role transfer. Seizure is used when the existing role holder cannot complete a normal transfer and the recovery circumstances justify the operation.

The exact historical command transcript and complete contemporaneous validation records are not included in this public case study.

## 4. 2025 — Infrastructure Modernization

The subsequent modernization addressed the legacy domain controller environment and established a replacement server configuration.

### Reported modernization sequence

1. Established a Windows Server 2016 domain controller.
2. Transitioned FSMO roles during the modernization sequence.
3. Managed DNS and DHCP service responsibilities within the updated environment.
4. Backed up the legacy server and copied the backup to a separate backup destination.
5. Rebuilt the existing physical server with Windows Server 2019 Standard.
6. Configured the rebuilt server as the replacement domain controller.
7. Transferred all five FSMO roles to the replacement Windows Server 2019 domain controller.

These steps describe the reported implementation sequence. They should not be interpreted as proof that every post-migration health check was independently completed or that all services were comprehensively tested.

## 5. Later Documented Service and Role Distribution

The later documented baseline was:

| Component | Reported configuration |
|---|---|
| Windows Server 2016 domain controller | AD DS and DNS |
| DHCP service | Remained on the Windows Server 2016 server |
| Replacement Windows Server 2019 domain controller | AD DS and DNS |
| FSMO roles | All five assigned to the replacement Windows Server 2019 domain controller |

**Important distinction:** Transferring FSMO roles does not transfer the DHCP server role, DHCP scopes, or DHCP configuration. DHCP service placement and configuration must be assessed separately.

This table represents the reported later baseline. It does not claim that all services were independently tested after the changes.

## 6. Representative Verification Commands

The following commands are reference examples for inspecting a comparable Active Directory environment. They are not presented as a historical execution transcript or proof that every check was run during this project.

### 6.1 Identify current FSMO role holders

Run from an appropriately configured domain-joined administrative system:

```cmd
netdom query fsmo
```

Review the output to identify the current holder of each of the five FSMO roles.

### 6.2 Assess domain controller diagnostics

```cmd
dcdiag /v
```

Review individual test results and investigate reported failures. Command completion alone does not establish that the domain controller is healthy.

### 6.3 Review DNS-related diagnostics

```cmd
dcdiag /test:dns /v
```

Use the results to investigate DNS registration, configuration, or connectivity issues.

### 6.4 Review replication status

```cmd
repadmin /replsummary
repadmin /showrepl
```

These commands provide replication summaries and inbound replication information. Interpret the output in the context of the domain topology and available replication partners.

### 6.5 Inspect installed Windows Server roles

Run in elevated PowerShell on the relevant server:

```powershell
Get-WindowsFeature AD-Domain-Services,DNS,DHCP
```

This helps identify whether the listed roles are installed. Role installation alone does not establish that the services are operating correctly.

### 6.6 Inspect relevant service states

```powershell
Get-Service NTDS,DNS,DHCPServer -ErrorAction SilentlyContinue
```

Review the returned states against the intended role distribution. Check DHCP on the server intended to provide the DHCP service.

### 6.7 Inspect Cisco DHCP relay configuration

On the relevant Cisco switch, use read-only commands appropriate to the platform and software version:

```text
show running-config | include ip helper-address
show ip interface vlan <VLAN-ID>
```

Replace `<VLAN-ID>` with the relevant VLAN identifier. Review the configured helper addresses and corresponding Layer 3 interface configuration.

Compare the configuration with the intended DHCP server address, VLAN design, routing, and network policy. A configured helper address alone does not prove successful DHCP allocation.

### Verification limitations

These commands are representative verification references. Their inclusion does not establish that they were executed during the historical incident or that their outputs were captured.

Actual verification requires suitable evidence, such as dated command output, relevant logs, or recorded test results. Any future validation should be documented separately from historical actions.

## 7. Operational Lessons

- Maintain a documented Active Directory recovery procedure that distinguishes metadata cleanup, FSMO role seizure, and normal FSMO transfer.
- Identify dependencies before recovery, including DNS, DHCP, authentication, VPN access, and network relay configuration.
- Document backup procedures and recovery prerequisites, including how backups can be accessed during an infrastructure failure.
- Plan domain controller replacement and role transitions as separate tasks with explicit validation criteria.
- Validate replication, DNS registration, authentication, and DHCP allocation after relevant changes.
- Record command output and timestamps so implementation actions can be distinguished from verified outcomes.
- Document administrative access and operational handover requirements to support traceability and future recovery.

## 8. Technologies

- Active Directory Domain Services (AD DS)
- FSMO role seizure and transfer
- Windows Server 2008 Standard
- Windows Server 2016 Standard
- Windows Server 2019 Standard
- DNS and DHCP
- Windows Server Backup
- Cisco core switching and DHCP relay
- Infrastructure incident recovery and modernization

## 9. Evidence and Disclosure

This public case study summarizes the reported implementation sequence and later service-role distribution. It excludes internal IP addresses, hostnames, domain identifiers, credentials, and backup-server names.

Historical actions are distinguished from representative verification commands. No command output, health-check result, or successful test is implied unless supported by appropriate evidence.

The document is a sanitized professional portfolio case study, not a complete production recovery runbook. Any real recovery must be planned against the actual environment, backup availability, replication state, and applicable operational controls.
