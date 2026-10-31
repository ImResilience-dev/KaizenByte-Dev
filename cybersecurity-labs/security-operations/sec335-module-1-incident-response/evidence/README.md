# Sanitized evidence summary

## Source inventory

| ID | Source | Directly inspected content |
|---|---|---|
| E1 | Conversation screenshot, filename time 17.22.50 on October 31, 2026 | ex261031.log: successful PASS responses in sessions 2/3 and repeated administrator failures in session 4 |
| E2 | Conversation screenshot, filename time 17.23.38 on October 31, 2026 | flag6.log: loopback records, challenge search, success-coded PASS entry |
| P1 | Learner-pasted Viewing Logs procedure | Directory navigation, dated-log selection, Notepad search for 230 |
| C1 | Learner statement | Lab completed |

Filename times are labels, not validated acquisition timestamps. Earlier activities appear in assistant summaries without their original scan or collection outputs.

## Published screenshots

- [E1 — dated FTP authentication log](ftp-authentication-log-redacted.png): original 1672 × 1852 pixels; black rectangle covering both sensitive PASS arguments.
- [E2 — loopback challenge log](ftp-loopback-challenge-redacted.png): original 1664 × 1396 pixels; black rectangle covering the numeric challenge answer.

These are redacted copies of the learner's screenshots, not recreated interfaces. Original dimensions and pixels outside the documented masks were checked.

Redaction rectangles use original-image coordinates with the top-left origin, inclusive start and exclusive end:

| Image | Rectangle (left, top, right, bottom) |
|---|---|
| E1 | (975, 250, 1177, 337) |
| E2 | (1424, 1258, 1604, 1314) |

Pixel comparison found **zero differences outside these rectangles**. SHA-256 values below identify the published redacted copies, not original acquisition evidence:

| Image | SHA-256 |
|---|---|
| E1 | a07d2c40e114d902e46b288167713dae5e4de19181c407ac93b4ebe7db0703ea |
| E2 | 39a376d0e0f63c4479f2d14a88fd5be8950d8428ce8030458d61e00d995e28ec |

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

- Unredacted screenshots, recovered passwords, sensitive PASS arguments, tokens, challenge values, and private transcripts are excluded. Redacted screenshot copies are included.
- E1's successful account is unknown because matching USER entries are not visible.
- E2 is a separate loopback artifact and does not establish success by E1's client.
- Original logs, acquisition hashes, clock validation, complete collection outputs, and grading results were unavailable.
- This summary records reviewed screenshot content; it is not a forensic image or chain-of-custody certificate.
