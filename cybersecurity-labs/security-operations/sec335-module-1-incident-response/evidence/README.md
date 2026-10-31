# Sanitized evidence summary

## Source inventory

| ID | Source | Directly inspected content |
|---|---|---|
| E1 | Conversation screenshot, filename time 17.22.50 on October 31, 2026 | ex261031.log: successful PASS responses in sessions 2/3 and repeated administrator failures in session 4 |
| E2 | Conversation screenshot, filename time 17.23.38 on October 31, 2026 | flag6.log: loopback records, challenge search, success-coded PASS entry |
| P1 | Learner-pasted Viewing Logs procedure | Directory navigation, dated-log selection, Notepad search for 230 |
| C1 | Learner statement | Lab completed |

Filename times are labels, not validated acquisition timestamps. Earlier activities appear in assistant summaries without their original scan or collection outputs.

## Sanitized excerpts

These are manually transcribed partial excerpts, not original log exports. [CLIENT] replaces the same non-loopback address throughout E1. [REDACTED] replaces the entire potentially sensitive PASS argument.

### E1 — dated log

    22:45:31 [CLIENT] [3]PASS [REDACTED] 230 0
    22:45:31 [CLIENT] [2]PASS [REDACTED] 230 0
    22:46:58 [CLIENT] [4]USER administrator 331 0
    22:46:58 [CLIENT] [4]PASS - 530 1326

The last two types of record repeat in the screenshot. No full-log total is inferred.

### E2 — challenge file

    03:57:19 127.0.0.1 [3]USER ftp 331 0
    03:57:22 127.0.0.1 [3]created /hi.txt 226 0
    03:57:19 127.0.0.1 [3]PASS - 230 [LAB CHALLENGE MARKER OMITTED]

These selected lines are not a reconstructed chronological sequence; the screen contains repeated entries.

## Limitations and privacy review

- Raw screenshots, recovered passwords, sensitive PASS arguments, tokens, challenge values, and private transcripts are excluded.
- E1's successful account is unknown because matching USER entries are not visible.
- E2 is a separate loopback artifact and does not establish success by E1's client.
- Original logs, acquisition hashes, clock validation, complete collection outputs, and grading results were unavailable.
- This summary records reviewed screenshot content; it is not a forensic image or chain-of-custody certificate.
