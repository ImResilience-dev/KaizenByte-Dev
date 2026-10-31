# SEC335 Module 1 — Incident Response Procedures, Forensics, and Forensic Analysis

| Field | Detail |
|---|---|
| Course | DeVry University — SEC335 |
| Author | ImResilience-dev |
| Status | Completed |
| Report date | October 31, 2026 |
| Environment | Authorized educational Windows lab |
| Focus | FTP authentication analysis and incident response reasoning |

## Overview

I completed this lab to practice interpreting authentication activity from an investigator's perspective. I examined Windows FTP logs, identified repeated administrator login failures, and compared those failures with successful FTP responses in separate sessions.

My main finding was a pattern consistent with password guessing against the administrator account. I also identified successful FTP responses, but the visible records did not establish that the administrator guessing sequence succeeded. This distinction shaped my analysis: I treated each record as evidence of a specific event rather than proof of a broader compromise.

## Scope and objectives

I limited this work to the authorized course lab. My objectives were to locate the FTP logs, interpret authentication records, identify suspicious patterns, and explain what additional evidence I would need before declaring a compromise.

The earlier lab discussion also referenced Nmap/Zenmap reconnaissance, a Bruter password exercise, RDP access, and incident response collection. The original outputs for those activities are not available with this report. I therefore focus my verified findings on the two retained screenshots and do not list scan results, recovered credentials, collection commands, or RDP outcomes as independently verified.

## My investigation process

The lab procedure directed me to the following FTP logging directory:

`C:\Windows\System32\LogFiles\MSFTPSVC1`

I reviewed the displayed records in **ex261031.log** and **flag6.log** in Notepad. The procedure called for searching for **230** to locate successful logins; my challenge screenshot also shows a search for the challenge marker.

I compared timestamps, client addresses, session identifiers, commands, and response codes. I kept the two files separate because their visible records represent different contexts. I did not assume that a success in one file explained failures in the other.

## Evidence and findings

### 1. Repeated administrator login failures

![Dated FTP log with sensitive password arguments redacted](evidence/ftp-authentication-log-redacted.png)

*Figure 1. My dated-log screenshot. A solid black rectangle covers the two potentially sensitive PASS arguments; the response codes remain visible.*

In Figure 1, I identified repeated **USER administrator** records with response **331**, followed by **PASS - 530 1326**, at the displayed time **22:46:58**. The same client address and session **[4]** appear repeatedly.

I interpreted this as a pattern consistent with password guessing. The repeated failures support that assessment, but the screenshot does not establish the complete number of attempts, the duration of the activity, or the tool responsible. I treated the recorded client address as a lab log field, not as proof of a person's identity or geographic location.

### 2. Earlier successful FTP responses

At **22:45:31**, Figure 1 also shows two **230 0** responses to PASS commands in sessions **[3]** and **[2]**, using the same recorded client address.

I identified these as successful FTP responses. However, the corresponding USER records are outside the visible excerpt, so I cannot identify the successful account from this screenshot. These successes also precede the displayed administrator failures. I cannot use them to conclude that the later administrator attempts succeeded.

### 3. Loopback activity in the challenge log

![Loopback FTP log with the numeric challenge answer redacted](evidence/ftp-loopback-challenge-redacted.png)

*Figure 2. My challenge-log screenshot. The answer is redacted; the loopback address, session identifier, and success response remain visible.*

In **flag6.log**, I identified a **PASS - 230** entry from **127.0.0.1**, session **[3]**, at **03:57:19**, alongside a lab challenge marker. Other visible records include **USER ftp**, **created /hi.txt**, and **QUIT**.

I recognized 127.0.0.1 as the loopback address. I therefore treated this as local lab activity rather than evidence that the client shown in Figure 1 gained access. The visible creation record also does not establish the file's contents or demonstrate exfiltration.

I located the challenge marker but have omitted its value from this public report. I do not claim a platform score or challenge-submission result.

### How I interpreted the codes

| Code | Meaning | How I used it |
|---|---|---|
| 331 | Server requests a password | I treated it as an intermediate step, not proof of valid credentials or a completed login. |
| 530 | Not logged in | I used it to identify failed FTP authentication. |
| 230 | User logged in | I identified success while checking the session and account context. |
| 1326 | Windows ERROR_LOGON_FAILURE | I used it as additional failure status accompanying 530. |

I checked FTP response meanings against [RFC 959](https://datatracker.ietf.org/doc/html/rfc959). Microsoft identifies 1326 as ERROR_LOGON_FAILURE in its [Windows support documentation](https://support.microsoft.com/en-us/servicing/os/windows-server/2017/01/error-1326-when-you-change-domain-account-password-in-windows).

## Discussion questions

**1. Where are the logs located in Windows?**

For this lab, I examined FTP logs in **C:\Windows\System32\LogFiles\MSFTPSVC1**. This is the FTP logging location used by this environment, not a universal location for all Windows logs. I would use Event Viewer to examine Windows application, security, and system events.

**2. What is stored in the MSFTPSVC1 directory?**

In this environment, it contains Microsoft FTP service log files. I used their timestamps, client addresses, session identifiers, commands, and response/status codes to examine authentication activity.

## My incident response recommendations

Based on these findings, my next steps in an actual investigation would be:

1. **Preserve the evidence.** I would retain the original FTP logs and relevant Windows events, document acquisition details and clock settings, calculate acquisition hashes, and analyze working copies.
2. **Correlate successful sessions.** I would locate the USER records for sessions [2] and [3], examine subsequent file operations, and check Windows authentication and remote-access events before asserting RDP access.
3. **Measure the activity.** I would use the complete dated log to establish attempt counts and time ranges rather than estimate them from a screenshot.
4. **Reduce exposure.** I would review whether FTP access is necessary, restrict privileged accounts, investigate affected credentials, and monitor repeated failures and unexpected successes.
5. **Address the legacy environment.** For production, I would use supported systems and a protected file-transfer service appropriate to the organization's requirements.

These are proposed actions; I am not claiming that I completed containment, credential rotation, or forensic acquisition in the documented portion of this lab.

## Evidence limits and handling

My available evidence consists of two screenshots and the supplied log-review procedure. I do not have the complete original logs, acquisition hashes, validated clock settings, or collection outputs. I report the screen times as displayed and do not combine the two files into a validated absolute timeline.

The screenshots retain their original dimensions, with no pixel changes outside the documented redaction rectangles. The [evidence record](evidence/README.md) contains sanitized excerpts, redaction coordinates, and hashes of the published image copies. Those publication hashes are not original acquisition hashes.

## What I learned

I learned to distinguish a suspicious pattern from a confirmed compromise. Repeated failures justified further investigation, but a successful response in another session did not prove administrator access. My strongest takeaway was to connect conclusions to the specific account, session, and time supported by the evidence—and to state clearly when that context is missing.
