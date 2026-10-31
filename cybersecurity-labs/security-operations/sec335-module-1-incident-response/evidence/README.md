# Screenshot index and handling record

## Course workflow references

These 19 figures accompanied the supplied lab instructions. They illustrate the exercise's topology, tools, and expected screens. Their dates, responder labels, and example counters belong to the course material; they are not a single continuous capture of my session.

| Screenshot | Subject |
|---|---|
| [topology.png](topology.png) | External attack topology |
| [nmap-scan.png](nmap-scan.png) | Initial port scan |
| [zenmap-profile.png](zenmap-profile.png) | Intense scan profile |
| [zenmap-services.png](zenmap-services.png) | Ports and detected services |
| [bruter-target.png](bruter-target.png) | FTP target and account |
| [bruter-dictionary-mode.png](bruter-dictionary-mode.png) | Dictionary mode |
| [bruter-wordlist.png](bruter-wordlist.png) | Wordlist selection |
| [bruter-start.png](bruter-start.png) | Configured dictionary test |
| [bruter-result-redacted.png](bruter-result-redacted.png) | Completed test; password redacted |
| [rdp-port-scan.png](rdp-port-scan.png) | Port 3389 scan |
| [rdp-client.png](rdp-client.png) | RDP client target |
| [rdp-desktop.png](rdp-desktop.png) | Remote server desktop |
| [server-topology.png](server-topology.png) | Internal server selection |
| [server-computer.png](server-computer.png) | Server navigation |
| [trusted-tools.png](trusted-tools.png) | IR_TOOLS command shell |
| [ir-network-output.png](ir-network-output.png) | Example IR.TXT network output |
| [ftp-log-search.png](ftp-log-search.png) | Search for response 230 |
| [windows-system32.png](windows-system32.png) | System32 navigation |
| [log-navigation.png](log-navigation.png) | Log-review navigation |

## My session captures

| Screenshot | Subject |
|---|---|
| [FTP authentication log](ftp-authentication-log-redacted.png) | ex261031.log: repeated administrator failures and earlier successful responses |
| [Loopback challenge log](ftp-loopback-challenge-redacted.png) | flag6.log: local FTP activity and challenge marker |

## Redaction record

I have excluded recovered password values and challenge answers from the published text and screenshots. Redacted PNGs preserve the original dimensions and have zero pixel differences outside the listed masks.

Coordinates use a top-left origin, inclusive starting coordinates and exclusive ending coordinates.

| Image | Original dimensions | Redaction rectangle (left, top, right, bottom) | Covered material |
|---|---|---|---|
| bruter-result-redacted.png | 653 × 559 | (347, 394, 415, 416) | Recovered password |
| ftp-authentication-log-redacted.png | 1672 × 1852 | (975, 250, 1177, 337) | Two sensitive PASS arguments |
| ftp-loopback-challenge-redacted.png | 1664 × 1396 | (1424, 1258, 1604, 1314) | Numeric challenge answer |

The other supplied PNGs are copied without image edits. No generated or reconstructed screenshot is included.

## File integrity

[SHA256SUMS](SHA256SUMS) identifies the published screenshot files. These publication hashes are separate from the lab's MD5 calculation of IR.TXT.

## Reading the log evidence

In the dated session capture, the repeated administrator failures occur in session [4]. The earlier success responses occur in sessions [2] and [3]. The separate challenge capture uses the loopback address. I keep those contexts distinct when interpreting the events.
