# Cryptography Techniques: Hashing, File Encryption, and BitLocker

## Overview

This authorized educational lab documents foundational data-protection techniques: hashing for integrity verification, file encryption for protecting data at rest, and BitLocker for full-disk encryption on supported Windows systems. The work emphasizes defensive use, secure key handling, and practical recovery planning.

## Learning Objectives

- Explain the difference between hashing and encryption.
- Use hashes to validate file integrity.
- Apply file-level encryption concepts to protect sensitive data.
- Explain how BitLocker protects data on a lost, stolen, or offline device.
- Identify key-management and recovery considerations.

## Lab Topics

| Topic | Purpose | Defensive Value |
| --- | --- | --- |
| Hashing | Create a fixed-length digest of data | Detect unintended or unauthorized file changes |
| File encryption | Protect selected files with cryptographic keys | Limit exposure when protected files are accessed or copied without authorization |
| BitLocker | Encrypt an entire Windows volume | Protect data at rest if a device is lost, stolen, or accessed offline |

## Security Considerations

- A hash is not encryption: it is designed to verify integrity, not to recover the original content.
- Encryption is only as strong as the protection of its keys, passwords, and recovery material.
- Store recovery keys securely and separately from the device they protect.
- Do not commit passwords, encryption keys, recovery keys, or sensitive encrypted files to source control.
- Test recovery procedures in an authorized environment before relying on them for important data.

## Repository Contents

- `notes.md` — Original lab documentation, exercises, observations, and key takeaways.

## Defensive Takeaways

- Verify the hashes of downloaded tools, evidence files, and important artifacts when trusted reference hashes are available.
- Use modern encryption and device-management practices to protect data at rest.
- Ensure recovery-key escrow, backup, and access-control procedures are documented before enabling full-disk encryption at scale.
- Treat secrets and recovery data as sensitive assets that must never be placed in public repositories.

## Authorized Use

This project documents authorized educational cybersecurity work. It is intended for defensive learning and data-protection practice only.
