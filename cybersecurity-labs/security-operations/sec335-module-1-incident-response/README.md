# SEC335 Module 1 — Incident Response Procedures, Forensics, and Forensic Analysis

| Field | Detail |
|---|---|
| Institution / course | DeVry University — SEC335 |
| Completion | Confirmed by the learner |
| Report prepared | October 31, 2026 |
| Scope | Authorized educational Windows lab |
| Evidence basis | Retrieved conversation, supplied lab procedure, and two directly inspected screenshots |

## Executive summary

This lab connected incident response with forensic interpretation of FTP authentication records. The learner confirmed completion. The directly available screenshots demonstrate repeated administrator login failures, separate successful FTP responses in the dated log, and a loopback success entry in a challenge file.

These observations support authentication analysis. They do not establish that the administrator password-guessing sequence succeeded, that RDP access occurred, or that data was exfiltrated.

## Objectives and scope

- Locate Microsoft FTP service logs in the supplied Windows environment.
- Interpret commands, response codes, client addresses, and session identifiers.
- Separate observations from hypotheses.
- Document evidence without publishing credentials.

This report covers authorized coursework only. No systems were tested during report preparation.

## Workflow and verification status

| Stage | Available basis | Status |
|---|---|---|
| Nmap / Zenmap reconnaissance | Earlier assistant progress summary | Reported in conversation; original output unavailable; ports and versions unverified |
| Bruter password exercise | Earlier assistant summary | Reported; original tool output unavailable; credentials excluded |
| RDP connection | Earlier assistant summary | Reported; not independently demonstrated by available evidence |
| Incident response collection | Summary and an ir2.txt window title visible behind the log windows | Contents, commands, results, and hashes unavailable |
| Windows FTP log analysis | Supplied procedure and two inspected screenshots | Directly demonstrated |
| Lab completion | Learner confirmation | Confirmed by learner; platform score unavailable |

The conversation reader returned no older-page cursor. Its handoff summary refers to earlier findings and integrity procedures, but the original artifacts were not available. Missing commands, scan findings, hashes, flags, and scores have not been reconstructed.

## Procedure: viewing logs

The supplied instructions directed navigation through **Computer → Local Disk (C:) → Windows → System32 → LogFiles → MSFTPSVC1**, opening the dated log in Notepad, then selecting **Edit → Find** and searching for **230**.

The screenshots show **ex261031.log** and **flag6.log** open in Notepad with the MSFTPSVC1 directory visible behind them. The challenge screenshot shows a search for the challenge marker. Not every prescribed click was captured.

## Verified findings

### Repeated administrator authentication failures

The dated-log screenshot shows repeated USER administrator entries with response 331, followed by PASS - 530 1326, at displayed time 22:46:58. The same recorded client address and session [4] recur.

This pattern is consistent with automated password guessing. The excerpt does not establish the full attempt count, duration, tool responsible, or operator identity. The recorded address is a lab log field, not a basis for geographic or real-world attribution.

### Successful responses require account and session correlation

The same screenshot shows two earlier PASS records with response 230 0 at 22:45:31, in sessions [3] and [2], using the same recorded client address. The PASS argument is withheld because it may contain credential material.

These entries show successful FTP responses, but their corresponding USER records are outside the visible excerpt. They precede the displayed administrator failures. They cannot identify the successful account or prove that the later administrator attempts succeeded.

### Loopback success in a challenge artifact

The second screenshot shows flag6.log with a PASS - 230 entry from 127.0.0.1, session [3], at 03:57:19, containing a deliberately inserted challenge marker. Other visible records include USER ftp, created /hi.txt, and QUIT.

This demonstrates a success-coded entry in a lab artifact. Its loopback source and separate file/session context prevent attributing it to the client in the dated log. A visible creation record alone does not establish file contents or external exfiltration.

The challenge marker was visually confirmed; its value is omitted from this portfolio. No submission acceptance, other challenge answers, or score is claimed.

### Response-code interpretation

| Code | Meaning | Relevance |
|---|---|---|
| 331 | Username accepted; password needed | Intermediate step, not proof of login |
| 530 | Not logged in | Failure response in the administrator attempts |
| 230 | User logged in | Success response requiring session/account correlation |
| 1326 | Windows ERROR_LOGON_FAILURE | Failure status accompanying 530 |

FTP meanings follow [RFC 959](https://datatracker.ietf.org/doc/html/rfc959). Microsoft identifies 1326 as ERROR_LOGON_FAILURE in its [Windows support documentation](https://support.microsoft.com/en-us/servicing/os/windows-server/2017/01/error-1326-when-you-change-domain-account-password-in-windows).

## Discussion questions

**1. Where are the logs located in Windows?**

In this lab, the FTP logs were examined at **C:\Windows\System32\LogFiles\MSFTPSVC1**.

This is the lab's FTP logging location, not a universal location for every Windows log. Application, security, and system event logs can be examined through Event Viewer.

**2. What is stored in the MSFTPSVC1 directory?**

In this environment, it contains Microsoft FTP service log files. The displayed records include event times, client addresses, session identifiers, FTP commands, and response/status codes. These fields help investigators distinguish failures from successes and correlate activity.

## Incident response implications

The following are recommended follow-up actions, not claims of work completed in this lab:

1. Preserve original FTP logs and relevant Windows events; document acquisition details and clock settings; analyze working copies.
2. Record cryptographic hashes at acquisition and transfer. No acquisition hash or chain-of-custody record was available for this report.
3. Correlate successful FTP sessions with USER records and file operations. Examine Windows authentication and remote-access events before concluding RDP access occurred.
4. Establish the complete attempt count and time range from full logs, keeping addresses, sessions, and accounts distinct.
5. Review FTP exposure, restrict administrative accounts, rotate affected credentials when warranted, and monitor authentication failures and successes.
6. Use supported systems and a protected file-transfer service appropriate to production requirements.

Times are reported as displayed. Without log timezone headers or clock validation, the two files cannot be combined into a reliable absolute timeline.

## Evidence and publication

The [sanitized evidence summary](evidence/README.md) contains the source inventory and credential-free excerpts. Original screenshots and raw logs are excluded because one screenshot contains a potentially sensitive PASS argument. Published excerpts omit that argument, challenge values, and unnecessary client-address details.

## Conclusion

The completed lab demonstrates how FTP records support incident investigation. Repeated administrator failures and separate success responses are visible. Neither an uncorrelated success code nor a loopback challenge entry proves that the displayed administrator guessing sequence compromised the server.
