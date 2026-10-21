# Mail Infrastructure — Mailcow, DNS, Security & Operations

## Project Overview

This project documents the deployment, administration, troubleshooting, and maintenance of a production Mailcow email platform hosted on Proxmox VE. It covers public email delivery, internal access, DNS authentication, directory integration, service validation, backup and recovery, storage migration planning, and operational training.

The documentation reflects actual project records and command evidence where available. Historical observations are identified as historical, and unresolved items are not represented as completed or verified.

> **Security notice:** This repository is a sanitized technical portfolio. Production IP addresses, internal network details, infrastructure identifiers, credentials, private keys, tokens, mailbox contents, and sensitive firewall or NAT configuration must not be published.

## Project Objectives

- Document the Mailcow deployment and its supporting virtualization infrastructure.
- Explain the relationship between external mail identity, internal access, and the configured Mailcow hostname.
- Document public DNS, SPF, DKIM, DMARC, reverse DNS, SMTP identity, and TLS verification.
- Provide repeatable CLI procedures for administration and troubleshooting.
- Document LDAP integration and its security boundaries.
- Preserve the evidence and recovery precautions associated with the planned 6 TiB root-disk migration.
- Provide structured MailOps training for account administration, sender permissions, and mailbox sharing.
- Separate verified outcomes, historical observations, planned work, and unresolved issues.

## Hostname Roles

The following names have distinct roles and must not be treated as interchangeable.

| Hostname | Documented role | Important qualification |
|---|---|---|
| `mail.alameen.com.sa` | External/public mail hostname | Public DNS, TLS, mail delivery, and reputation must be revalidated when making current-state claims. |
| `mail.nameen.com` | Internal access hostname | Internal reachability and certificate coverage must be verified independently. |
| `mailcow.nameen.com` | Configured Mailcow primary hostname recorded in project evidence | Confirm the live configuration before changing the hostname or drawing conclusions about current service identity. |

The external hostname is the intended public-facing identity. The internal access hostname is documented separately. A successful HTTPS response for one hostname does not prove that the other hostname has valid TLS coverage or is reachable from the same networks.

## Architecture Overview

The platform combines a containerized mail application with a virtualized Linux host and supporting network services.

```text
                         Internet
                            |
              Public DNS and Email Services
                            |
                mail.alameen.com.sa
                            |
                 Public Network Boundary
                  (NAT / Firewall)
                            |
                  Proxmox VE Platform
                            |
                    Linux Mail VM
                            |
                    Mailcow Docker
                            |
       +--------------------+--------------------+
       |                    |                    |
   SMTP / Mail          Webmail / SOGo      Mail Storage
   Delivery             User Access         and Databases
       |
       +---------- Directory Integration
                  (LDAP, if applicable)
```

This diagram is conceptual. It does not disclose production IP addresses, NAT mappings, physical node names, VM identifiers, or storage topology.

## Core Technologies

- **Mail platform:** Mailcow Dockerized
- **Operating system:** Debian 12, as recorded in the project documentation
- **Virtualization:** Proxmox VE
- **Container orchestration:** Docker Compose
- **Webmail and groupware:** SOGo
- **Directory integration:** LDAP
- **Public DNS and email authentication:** A, MX, TXT, SPF, DKIM, DMARC, and PTR records
- **Transport security:** HTTPS and SMTP TLS
- **Storage and recovery:** Linux filesystems, backup archives, snapshots, and controlled migration procedures

Component versions and live configuration must be collected again before this document is used as a current-state inventory.

## Mail Flow and DNS

The documented public mail identity is `mail.alameen.com.sa`, with the domain `alameen.com.sa` using that hostname as its recorded MX destination.

The following records were documented historically:

| Record | Historical finding | Current status |
|---|---|---|
| A | Public hostname resolved to a production public IP | Recheck; IP intentionally omitted |
| MX | `alameen.com.sa` pointed to `mail.alameen.com.sa` with priority 10 | Recheck |
| SPF | Policy used an IPv4 mechanism and `-all` | Recheck the actual public record |
| DKIM | Selector recorded as `dkim` | Current public key and signature validation must be verified |
| DMARC | `v=DMARC1; p=none` | Recheck policy and reporting configuration |
| PTR | Historical reverse DNS aligned with `mail.alameen.com.sa` | Recheck |
| SMTP HELO | Recorded as `mail.alameen.com.sa` | Verify the effective live setting |

Historical DNS observations were recorded around 11 October 2026. They are not proof that the records remain unchanged.

A previous DKIM PASS result for the old hostname `mail.ameen-co.com` must not be attributed to `mail.alameen.com.sa`. Authentication must be tested using a new controlled message and the receiving system's `Authentication-Results` header.

See [`docs/mail-flow-and-dns.md`](docs/mail-flow-and-dns.md).

## TLS and Network Access

HTTPS and Let's Encrypt operation were reported as working after the hostname migration. A historical certificate check for `mail.alameen.com.sa` recorded a validity period from 13 October 2026 through 11 January 2027.

These are dated findings, not a guarantee of current certificate validity. They do not establish certificate coverage for `mail.nameen.com` or `mailcow.nameen.com`.

Recorded service-port requirements included:

- TCP 25 — SMTP delivery
- TCP 80 — HTTP and certificate-related access, as applicable
- TCP 443 — HTTPS
- TCP 465 — SMTP submission over implicit TLS
- TCP 587 — SMTP submission with STARTTLS
- TCP 993 — IMAPS

Actual exposure depends on current firewall, NAT, service-listener, and routing configuration. The port list is not evidence that every port is presently reachable from the Internet.

See [`docs/tls-and-firewall.md`](docs/tls-and-firewall.md).

## Directory Integration

Project records document an LDAP connection to the internal NAMEEN directory using a read-only service account.

The recorded configuration included:

- Directory domain: `nameen.com`
- Base DN: `DC=nameen,DC=com`
- Username attribute: `userprincipalname`
- LDAP transport: TCP 389
- Automatic account creation/import and full synchronization: disabled
- Synchronization interval: 15 minutes
- Connection test: reported successful in the project evidence

Private directory server addresses and service-account details are excluded.

A successful connection test does not independently establish secure transport, successful user authentication, or correct authorization. LDAPS or STARTTLS remains future work unless subsequently implemented and verified.

See [`docs/ldap-integration.md`](docs/ldap-integration.md).

## Operations and Troubleshooting

Operational checks should establish the current state before any production change.

Example commands:

```bash
hostname -f
ip -br address
ip route
findmnt /
df -hT

cd /opt/mailcow-dockerized
sudo docker compose config -q
sudo docker compose ps
```

The commands above collect host identity, network state, filesystem information, Compose configuration validity, and container status. They do not by themselves prove successful end-to-end email delivery.

### Documented Message-Size Error

A `5.3.4 Error: message file too big` error was reported on 15 October 2026. The component enforcing the limit was not conclusively identified in the available evidence.

Diagnostic commands:

```bash
cd /opt/mailcow-dockerized

sudo docker compose ps

sudo docker compose exec -T postfix-mailcow \
  postconf message_size_limit mailbox_size_limit

sudo docker compose logs --since=30m postfix-mailcow
sudo docker compose logs --since=30m nginx-mailcow
sudo docker compose logs --since=30m php-fpm-mailcow
```

The next step is to correlate the exact rejection, timestamp, message size, and submission path with the relevant logs and effective limits. Do not increase limits or restart all services without identifying the enforcing component and assessing the impact.

See [`docs/troubleshooting.md`](docs/troubleshooting.md).

## Backup, Recovery, and Storage Migration

The project includes a runbook for migrating the mail VM's root filesystem to a larger 6 TiB target disk.

At the documented checkpoint:

- The original root disk remained the known active system disk.
- The target disk had been prepared and mounted for migration work.
- A snapshot-mode VM backup archive of approximately 4.52 GB passed a structural integrity test.
- A restore test had not been completed.
- QEMU Guest Agent was not configured in the recorded state.
- The final root-disk cutover was incomplete.
- Existing recovery snapshots and the original disk were to be preserved.

Consequently, the documentation does not claim that the migration is complete, that the backup is application-consistent, or that restoration has been proven.

Any cutover requires a controlled maintenance procedure, a final data synchronization, reviewed boot and filesystem configuration, post-boot service acceptance tests, and a defined rollback path. The original disk, required snapshots, and backup must not be removed before formal acceptance.

See [`docs/storage-migration-and-recovery.md`](docs/storage-migration-and-recovery.md).

## MailOps Training

Five training modules are included to support controlled, least-privilege administration.

1. [Module 01 — Interface Familiarization and Access](training/modules/module-01-interface-access.md)
2. [Module 02 — Accounts, Least Privilege, and TFA/MFA](training/modules/module-02-accounts-mfa.md)
3. [Module 03 — Multiple Sender Addresses and Send As](training/modules/module-03-send-as.md)
4. [Module 04 — User-Level Sender Delegation and From Selection](training/modules/module-04-sender-delegation.md)
5. [Module 05 — Inbox Sharing and Shared Folders](training/modules/module-05-mailbox-sharing.md)

The [Complete MailOps Training Manual](training/complete-training-manual.md) consolidates the training approach, readiness checks, evidence requirements, and trainee/trainer assessment.

Training material describes procedures and verification requirements. It does not prove that a particular feature, permission, or administrative route is enabled in the installed Mailcow release.

For example, the proposed IT department Send As arrangement is a target use case, not evidence of a completed production permission change.

## Evidence and Verification Standards

Technical records use the following distinctions:

- **Verified:** Supported by identifiable command output, test results, or other direct evidence.
- **Historically observed:** Reported or captured at a specific earlier checkpoint; requires revalidation before being described as current.
- **Planned:** Proposed but not confirmed as implemented.
- **Unresolved:** Available evidence does not establish the outcome.
- **Not tested:** A procedure or acceptance test has not been executed or its result is unavailable.

Configuration validity, service availability, external reachability, successful authentication, and successful mail delivery are different outcomes. Evidence for one must not be used to claim the others.

Sensitive evidence should be retained in an appropriately restricted location rather than committed to this public portfolio.

## Security and Privacy

Before publishing changes, ensure the repository excludes:

- Production public and private IP addresses and internal network ranges
- VM IDs, infrastructure node names, storage identifiers, disk UUIDs, and private mount paths
- Passwords, password hashes, tokens, session cookies, and private keys
- Full DKIM private-key material and sensitive service-account configuration
- Mailbox contents, personal information, and message headers containing sensitive data
- Detailed production firewall rules, NAT mappings, and internal routing information
- Unredacted backup paths or other infrastructure-specific identifiers

Public hostnames are included where needed to explain the architecture. Their inclusion does not imply that DNS, TLS, or mail authentication has been freshly verified.

## Project Outcomes and Lessons Learned

The project records demonstrate hands-on work with Mailcow administration, Proxmox virtualization, public mail identity, DNS and email authentication, LDAP integration, troubleshooting, backup validation, and storage migration planning.

Key operational lessons include:

- Separate external service identity from internal access and application configuration.
- Revalidate SPF, DKIM, DMARC, PTR, HELO, and TLS independently after hostname changes.
- Investigate the component enforcing a limit before modifying production configuration.
- Treat a structurally valid backup as distinct from a successfully restored backup.
- Preserve rollback options until the migrated system has passed acceptance testing.
- Apply least privilege and verify the actual behavior of Send As, delegation, MFA, and shared-mailbox features.
- Maintain an auditable distinction between configuration, execution, and verified outcome.

## Supporting Documentation

| Document | Purpose |
|---|---|
| [Architecture and Deployment](docs/architecture-and-deployment.md) | Platform architecture, deployment context, host checks, and configuration validation |
| [Mail Flow and DNS](docs/mail-flow-and-dns.md) | Public mail identity, DNS records, SPF, DKIM, DMARC, PTR, and delivery testing |
| [TLS and Firewall](docs/tls-and-firewall.md) | Certificate validation, service ports, network access, and safe verification |
| [LDAP Integration](docs/ldap-integration.md) | Directory configuration, connection testing, and security considerations |
| [Troubleshooting](docs/troubleshooting.md) | Operational checks, logs, message-size investigation, and acceptance testing |
| [Storage Migration and Recovery](docs/storage-migration-and-recovery.md) | 6 TiB migration procedure, backup evidence, acceptance, and rollback |
| [MailOps Training](training/README.md) | Training index and assessment guidance |

---

**Documentation status:** Portfolio documentation based on the available project records. Historical observations are explicitly identified, and outstanding verification or migration tasks remain open until supported by new evidence.
