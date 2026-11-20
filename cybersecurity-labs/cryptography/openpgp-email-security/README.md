# Implement OpenPGP — Email Encryption, Digital Signatures, and Key Management

**Course:** SEC399 — Systems Security Certified Practitioner, DeVry University  
**Lab:** Implement OpenPGP (ISC2-CISSP)  
**Completion date:** November 19, 2026  
**Environment:** Authorized Practice Labs Windows virtual machines  
**Status:** Completed (student-confirmed)

## Objective

Develop hands-on familiarity with OpenPGP certificate creation, public-key distribution, digital signatures, certificate importation and certification, and encrypted email workflows. This report documents a completed educational exercise, not a production security assessment.

## Tools

- **Gpg4win 2.3.3:** OpenPGP software supplied by the exercise
- **Kleopatra:** Manage OpenPGP certificates and keys
- **GpgOL:** Sign, encrypt, and decrypt Outlook messages
- **GPA:** GNU Privacy Assistant (installation component)
- **Outlook 2013:** Lab email client
- **PLABCAS01 and PLABCAS02:** Isolated Practice Labs hosts

> Gpg4win 2.3.3 and Outlook 2013 are legacy lab software, not recommended production versions.

## Exercise 1 — Install OpenPGP

Prepared the prescribed virtual machines, created a Windows network share on PLABCAS02, and used it to access the Gpg4win installer from PLABCAS01. Completed the installation with GPA enabled.

Example PowerShell commands adapted from the lab:

```powershell
New-Item -Path C:\Share -ItemType Directory
NET SHARE Share=C:\Share
```

The shared folder was accessed with a UNC path (`\\PLABCAS02\Share`). Windows SMB commonly uses **TCP 445**.

**Lesson:** Endpoint preparation and controlled software distribution are prerequisites for reliable cryptographic workflows.

## Exercise 2 — Certificate Creation and Distribution

Used Kleopatra to generate the Administrator test identity's OpenPGP key pair, using the lab's default **RSA 2048-bit** configuration. Reviewed certificate details and its fingerprint, followed the key-pair backup procedure, exported the **public certificate**, and attached it to an email addressed to the second lab identity.

**Lesson:** Public keys are designed to be shared, but private keys must be safeguarded. A public-key fingerprint can help detect key substitution when checked against a trusted source. The lab's demonstration passphrase and backup location are **not** appropriate production practices.

## Exercise 3 — Signing and Importation

Used the GpgOL signing function in Outlook to digitally sign a message with the Administrator's private key. Switched to the Lisa Scott test account, saved the received public certificate, imported it into Kleopatra, and prepared a separate OpenPGP identity for Lisa.

**Lesson:** Digital signatures support message integrity and authentication of the signing key. They do **not** provide message confidentiality by themselves. The sender's **private key signs**; others use the sender's **public key to verify**.

## Exercise 4 — Verification, Encryption, and Decryption

In Kleopatra, selected the imported Administrator certificate, followed the fingerprint verification workflow, and chose **Certify only for myself**. Used Outlook's GpgOL **Encrypt** action to send an encrypted message from Lisa to the Administrator, with Lisa's public certificate attached. Returned to the Administrator account and used the associated private key and passphrase to decrypt the received message.

**Lesson:** A sender encrypts to the **recipient's public key**; the recipient decrypts with their **private key**. Importing a certificate is not proof of ownership by itself: fingerprint verification through an independent trusted channel is a valuable control.

## Key Concepts

| Concept | Application |
| --- | --- |
| Confidentiality | Encrypt message contents to prevent unauthorized reading |
| Integrity | Verify digital signatures to detect changes in signed content |
| Authentication | Establish confidence in the identity-to-public-key association |
| Nonrepudiation | Signatures can support attribution when private-key custody and identity verification are reliable |
| Certificate fingerprint | Key identifier for comparing against a trusted reference |
| Certificate certification | Records trust in an identity-to-key binding |
| Key management | Generation, secure storage, backup, rotation, and revocation |

OpenPGP ordinarily uses **hybrid encryption**: asymmetric cryptography protects a session key, while symmetric encryption protects the message contents.

**Memory aid:** Private key signs; public key verifies. Recipient's public key encrypts; recipient's private key decrypts.

## Network Port Reference

OpenPGP itself does not require a dedicated transport port. Relevant supporting services include:

| Service | Common port | Lab relevance |
| --- | --- | --- |
| SMB | TCP 445 | Windows shared-folder installer transfer |
| SMTP submission | TCP 587 | Common outgoing email submission |
| SMTP relay | TCP 25 | Mail-server delivery |
| IMAPS | TCP 993 | Secure email retrieval |
| HTTPS | TCP 443 | Web services and some keyserver endpoints |

The lab materials do not establish which email transport ports Outlook used in this particular environment.

## Results and Reflection

All four exercises were reported completed on **November 19, 2026**. The lab demonstrated how OpenPGP key pairs, certificate distribution, digital signatures, trust decisions, and email encryption/decryption fit into a single workflow.

The main takeaway was that cryptographic security involves more than strong algorithms. Proper protection of private keys, identity verification, certificate lifecycle management, and backup practices are essential for secure communication. Hands-on work helped connect these concepts to practical Windows administration and email security.

**Evidence note:** This report does not claim independently collected validation screenshots, command output, or packet captures. No actual secret keys or passphrases are included.

## Reference

Wills, M. S. (2022). *SSCP systems security certified practitioner official study guide* (3rd ed.). Sybex.

---

*KaizenByte — Learn. Build. Defend. Improve.*
