# Active Directory Breach Analysis

## Overview

This project provides a portfolio-ready structure for documenting an authorized Active Directory security lab. Its focus is defensive analysis: identifying likely attack paths, reviewing security-relevant evidence, and translating observations into practical hardening and response recommendations.

The original lab report remains at the repository root until its contents can be safely recovered and migrated into this folder.

## Learning Objectives

- Identify common Active Directory security risks in an authorized lab environment.
- Understand the importance of privileged identities, authentication controls, directory permissions, and domain-controller security.
- Document security observations without exposing credentials, sensitive host details, or personal data.
- Map findings to practical detection, containment, and hardening actions.
- Communicate an incident-analysis workflow in a clear, professional format.

## Scope and Authorization

All testing, investigation, and evidence collection must occur only in an isolated educational lab or another environment where explicit authorization has been granted. This project is for defensive-security learning and documentation; it must not be used against systems, accounts, domains, or networks without permission.

## Investigation Workflow

| Phase | Defensive objective | Examples of documented evidence |
| --- | --- | --- |
| Scoping | Establish authorized targets and boundaries | Lab diagram, scope statement, approved test accounts |
| Triage | Identify suspicious behavior or high-risk conditions | Authentication anomalies, privileged-group changes, unusual account activity |
| Analysis | Correlate observations and assess impact | Sanitized event logs, directory-permission review, timeline of events |
| Containment | Limit exposure and preserve evidence | Account restrictions, host isolation, credential reset plan |
| Recovery | Restore a trusted security baseline | Privilege review, patching, monitoring validation, backup verification |
| Lessons learned | Improve resilience and detection | Control gaps, recommended alert rules, policy improvements |

## Key Security Areas

### Privileged Access

- Limit membership in high-privilege groups and review it regularly.
- Use separate administrative accounts for privileged work.
- Apply least privilege and role-based access controls.
- Protect domain-controller administration with strong authentication and restricted access paths.

### Authentication and Credentials

- Use long, unique passwords and multi-factor authentication where supported.
- Monitor for repeated failed authentication followed by success.
- Disable stale accounts and promptly remove access when roles change.
- Rotate credentials and investigate potentially exposed privileged accounts.

### Logging and Detection

- Forward security logs to a centralized platform such as a SIEM.
- Monitor changes to privileged groups, account creation, account disablement, and unusual login patterns.
- Establish baselines for administrator logons and service-account behavior.
- Preserve relevant logs and timestamps to support incident timelines.

### Hardening and Recovery

- Keep domain controllers patched and minimize installed software and exposed services.
- Use tested, protected backups and document recovery procedures.
- Segment administrative systems from standard user workstations.
- Periodically test incident-response and recovery workflows in an authorized lab.

## MITRE ATT&CK Context

| Area | Technique | Defensive relevance |
| --- | --- | --- |
| Credential Access | [T1003: OS Credential Dumping](https://attack.mitre.org/techniques/T1003/) | Protect credential material and detect suspicious access to credential stores. |
| Privilege Escalation | [T1078: Valid Accounts](https://attack.mitre.org/techniques/T1078/) | Monitor use of valid but compromised accounts, especially privileged identities. |
| Discovery | [T1087: Account Discovery](https://attack.mitre.org/techniques/T1087/) | Review for abnormal account-enumeration activity in authorized monitoring data. |

## Evidence Guidance

When the original report or approved screenshots are available, store sanitized artifacts in an `evidence/` directory. Before committing any artifact, remove or obscure:

- Passwords, hashes, tokens, API keys, or recovery material.
- Internal IP addresses, hostnames, domain names, and unique environment identifiers when they are not intended for public release.
- Personal information and student or employee account details.
- Unredacted event logs or configuration exports containing sensitive values.

## Suggested Folder Contents

```text
active-directory-breach-analysis/
├── README.md
├── notes.md
├── mitigations.md
└── evidence/
```

## Defensive Takeaways

- Treat Active Directory as a high-value identity system and prioritize protection of privileged accounts and domain controllers.
- Detecting abnormal authentication patterns and privilege changes early reduces the chance of widespread compromise.
- Strong logging, centralized analysis, segmentation, and tested recovery processes are essential layers of domain defense.
- Documented authorization and careful evidence sanitization are required for responsible public security portfolios.

## Authorized Use

This project documents authorized educational cybersecurity work. It is intended exclusively for defensive learning, security analysis, and responsible lab documentation.
