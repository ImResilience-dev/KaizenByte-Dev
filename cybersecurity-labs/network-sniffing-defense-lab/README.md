# Network Sniffing Defense Lab: MAC Flooding and DNS Poisoning

## Overview

This project provides a defensive-security structure for an authorized networking lab focused on packet-capture risks, MAC flooding, and DNS poisoning. The goal is to recognize relevant indicators, understand how these conditions can affect confidentiality and network availability, and document layered mitigations.

The original lab report remains at the repository root until its contents can be safely recovered and migrated into this folder.

## Learning Objectives

- Explain the security implications of unauthorized packet capture.
- Identify the network impact of MAC address table exhaustion or flooding.
- Recognize the risks associated with DNS spoofing or poisoned DNS responses.
- Document evidence and observations only from an authorized, isolated lab.
- Recommend practical controls for switching infrastructure, DNS, monitoring, and user protection.

## Scope and Authorization

All activities must be limited to a controlled educational environment or another explicitly authorized network. This repository is for defensive learning, documentation, detection, and mitigation planning only. Do not intercept traffic, disrupt switching behavior, alter DNS responses, or test systems without explicit permission.

## Threat Areas

| Area | Risk | Potential impact |
| --- | --- | --- |
| Packet capture | Traffic is observed without authorization | Exposure of unencrypted credentials, session data, or sensitive communications |
| MAC flooding | A switch's forwarding table is overwhelmed with spoofed source addresses | Unintended traffic flooding, degraded performance, or greater opportunity for interception |
| DNS poisoning | A resolver or client accepts a malicious or incorrect DNS response | Users may be redirected to fraudulent or unsafe destinations |

## Detection and Analysis

### Packet-Capture Risk

Defensive indicators may include unexpected promiscuous-mode interfaces, unapproved monitoring devices, unusual network-interface configuration changes, and sensitive protocols observed in clear text. Use authorized packet captures and sanitized evidence only.

### MAC Flooding Indicators

- Rapid growth or churn in learned MAC addresses on a switch port.
- Large volumes of frames with changing or implausible source MAC addresses.
- Broadcast or unknown-unicast traffic increases.
- Switch security alerts, port-security violations, or unexpected interface errors.

### DNS Poisoning Indicators

- DNS answers that do not match trusted records or expected resolver behavior.
- Unexpected changes in DNS-server configuration.
- Certificate warnings, redirects, or domain-resolution inconsistencies.
- Client requests to unfamiliar destination IP addresses immediately after DNS lookup.

## Defensive Controls

| Control area | Recommended practices |
| --- | --- |
| Switching | Enable port security where appropriate, set MAC-address limits, disable unused ports, and segment networks with VLANs |
| Traffic confidentiality | Use encrypted protocols such as HTTPS, SSH, SFTP, and secure email rather than clear-text alternatives |
| DNS security | Use trusted resolvers, enable DNSSEC validation where supported, restrict recursive resolution, and monitor configuration changes |
| Monitoring | Centralize switch, DNS, endpoint, and authentication logs; alert on port-security events and unusual DNS patterns |
| Access control | Apply least privilege to network administration and restrict access to management interfaces |
| User protection | Train users to recognize certificate warnings, phishing sites, and suspicious redirects |

## MITRE ATT&CK Context

| Area | Technique | Defensive relevance |
| --- | --- | --- |
| Credential Access | [T1040: Network Sniffing](https://attack.mitre.org/techniques/T1040/) | Protect sensitive communications with encryption and investigate suspicious traffic-capture activity. |
| Adversary-in-the-Middle | [T1557: Adversary-in-the-Middle](https://attack.mitre.org/techniques/T1557/) | Monitor for conditions that could enable traffic interception or manipulation. |
| Discovery | [T1016: System Network Configuration Discovery](https://attack.mitre.org/techniques/T1016/) | Monitor authorized environments for unusual network-configuration discovery activity. |

## Evidence Guidance

When the original report or approved lab artifacts are available, store sanitized material in an `evidence/` directory. Before committing, remove or obscure:

- Credentials, cookies, session identifiers, API keys, and tokens.
- Private hostnames, internal IP addresses, MAC addresses, and DNS records not intended for public release.
- Personal or organization-specific information.
- Raw packet captures unless public sharing is explicitly authorized and sensitive payloads have been removed.

## Suggested Folder Contents

```text
network-sniffing-defense-lab/
├── README.md
├── notes.md
├── mitigations.md
└── evidence/
```

## Defensive Takeaways

- Encrypting sensitive network traffic limits the impact of packet capture.
- Switch-port security, segmentation, and monitoring reduce the risk and visibility created by MAC flooding.
- DNS hardening, trusted resolution, and user awareness reduce exposure to poisoned or manipulated name resolution.
- A strong network-defense program combines secure configuration, telemetry, alerting, and incident-response planning.

## Authorized Use

This project documents authorized educational cybersecurity work. It is intended exclusively for defensive learning, network analysis, detection, and mitigation practice.
