# SEC335 Module 2 — Introduction to Autopsy Forensic Browser

**Portfolio:** KaizenByte • **Discipline:** Digital forensics  
**Lab completion:** November 8, 2026, explicitly confirmed by the learner  
**Environment:** Autopsy 3.0.8 on a Windows 7 training virtual machine  
**Outcome:** All five challenge flags solved, as reported by the learner

## Executive summary

This first completed SEC335 Module 2 lab introduced forensic case setup, examination of E01 evidence images, file and image review, and extraction of PNG flag artifacts using Autopsy. The exercise used the case name **NTFS Capture**, base directory **H:\\Case**, case identifier **Lab07**, and examiner **Student**. The examined evidence images were **ntfs_pract.E01** and **flags.E01**.

The learner reports reviewing image and file artifacts, extracting PNG flag files, and solving all five challenges. This write-up documents that training workflow and its evidentiary limits. It is a retrospective portfolio report, not an independently reproduced examination or an Autopsy-generated export.

## Scope and source basis

The source conversation is titled *SEC335 Incident Response and Digital Forensics*. The learner's continuation request explicitly identifies this exercise as **Introduction to Autopsy Forensic Browser**, supplies the environment and case details above, and confirms completion on November 8, 2026.

During preparation, the available conversation reader returned only the later Hashing Data Sets portion and references to image attachments without image contents. The earlier detailed Autopsy instructions and original screenshots were not available for direct inspection. Consequently, the case details and outcomes below are attributed to the learner's supplied account. No screenshot-specific observations, exact challenge answers, artifact paths, timestamps, or file counts have been reconstructed.

This report covers only the Autopsy exercise. EnCase acquisition, Kali hashing, HashCalc, and their challenge answers belong to the separate **Hashing Data Sets** lab.

## Objectives and skills

- Configure an identifiable forensic case and examiner record.
- Examine supplied E01 images through a forensic analysis interface.
- Navigate file artifacts and review image content.
- Extract relevant PNG files for examination.
- Distinguish a reported lab result from independently verifiable forensic evidence.

## Case and evidence register

| Field | Recorded value | Basis |
| --- | --- | --- |
| Case name | NTFS Capture | Learner-supplied lab details |
| Base directory | `H:\Case` | Learner-supplied lab details |
| Case identifier | Lab07 | Learner-supplied lab details |
| Examiner | Student | Training identifier supplied by learner |
| Tool | Autopsy 3.0.8 | Learner-supplied environment |
| Operating system | Windows 7 training VM | Learner-supplied environment |
| Evidence image 1 | `ntfs_pract.E01` | Reported as examined |
| Evidence image 2 | `flags.E01` | Reported as examined |
| Derived artifacts | Extracted PNG flag files | Reported extraction; exact filenames and destinations unavailable |
| Completion | Five of five challenge flags solved | Learner-confirmed outcome; no independent grading record inspected |

The base directory is a training case location, not a verified source-evidence path. The supplied case name and case identifier are retained as distinct fields; the full generated case-folder path has not been verified.

## Forensic workflow

### 1. Prepare the analysis environment

The exercise used Autopsy 3.0.8 within the Windows 7 training VM. This records the historical lab environment rather than asserting suitability for a current production investigation. Installation success is part of the learner's completed-lab account; an installer log or version screenshot was not independently inspected for this report.

### 2. Establish the case

The recorded configuration was **NTFS Capture**, with **H:\\Case** as the base directory, **Lab07** as the case identifier, and **Student** as examiner. These fields establish organizational context for analysis and help separate case output from source evidence.

### 3. Examine the supplied images

The learner examined **ntfs_pract.E01** and **flags.E01** in Autopsy. The reported workflow involved navigating file artifacts and reviewing images to locate information relevant to the lab challenges.

Exact ingest-module selections, processing logs, image sizes, partition layouts, deleted-file status, and whether both sources were added to the same case are not independently established by the available record. No such details are inferred here.

### 4. Review artifacts and extract PNG files

The learner reviewed images and file artifacts, then extracted PNG flag files for examination. Extraction produces derived files that should remain traceable to the source image and source artifact. The available account does not establish which challenge corresponded to each PNG, or that every challenge answer came from a PNG.

### 5. Complete the challenges

All five challenge flags were reported solved, and the learner explicitly confirmed that the lab was complete on **November 8, 2026**. Exact flag strings are omitted. The completion statement is a learner-confirmed training outcome; it is not presented as independently observed challenge-platform acceptance.

## Evidence handling

The analysis described here used supplied evidence images rather than documenting a new acquisition of physical media. No claim is made that this exercise established acquisition provenance, used a hardware write blocker, or produced a complete chain of custody.

For a reproducible examination, the evidence record should retain source-image identifiers, cryptographic hashes, processing settings, examiner actions, original artifact paths, and extraction destinations. Originals should be preserved, with analysis and exported artifacts kept separately. These are recommended handling practices, not actions independently verified in this lab.

No source-image hashes or export hashes were supplied for independent comparison. The E01 extension alone does not establish that integrity verification ran successfully. GitHub version history records changes to this portfolio document; it does not authenticate the original forensic evidence.

## Findings and confidence

| Finding | Supported conclusion | Limitation |
| --- | --- | --- |
| Case setup | Learner records the NTFS Capture / Lab07 configuration | Case database and setup screenshot unavailable for inspection |
| Evidence examination | Learner reports examining both named E01 images | No independent examination of image contents performed |
| Artifact review | Images and file artifacts were reviewed | Exact content, paths, metadata, and counts unavailable |
| PNG extraction | PNG flag files were extracted | Exported bytes and source-to-export mapping unavailable |
| Challenge outcome | All five flags solved; lab complete November 8, 2026 | Learner confirmation; grading evidence not directly inspected |

These results support a training account of case organization, artifact examination, and file extraction. They do not support conclusions about a real incident, attribution, malware, data theft, or the activity of a particular person.

## Screenshots and supporting material

See the [evidence availability note](evidence/README.md). No screenshots are embedded in this revision because the original Autopsy attachments could not be retrieved for inspection and sanitization. Images from the later Hashing Data Sets lab have not been substituted.

The portfolio contains no E01 images, case database, recovered PNG flag contents, exact challenge solutions, credentials, or private course-session details.

## Lessons learned

1. **Case organization supports traceability.** A case name, identifier, examiner, and output location make the analysis easier to document and revisit.
2. **Artifact context matters.** A useful finding includes its source image, original path, relevant metadata, and the method used to inspect or extract it.
3. **Exports need their own record.** Recovered files are derived artifacts; retaining their relationship to the source is essential.
4. **Completion and verification are different records.** A learner's completion confirmation can document progress, while independent forensic conclusions require preserved evidence and reproducible checks.

## Limitations and next documentation steps

This report was prepared without direct access to the original evidence images, case database, exported PNGs, full earlier instructions, or Autopsy screenshots. It does not claim verified hash matches, a complete chain of custody, a particular ingest configuration, exact challenge values, or generation of an Autopsy HTML/PDF report.

To strengthen the portfolio evidence, add inspected and sanitized screenshots of case configuration, evidence-source navigation, artifact review, extraction, and challenge completion. Captions should distinguish learner screenshots from instructional examples. Preserve private originals separately; redact flag values and unrelated account or session information in published copies.

---

*Authorized educational training exercise. Retrospective report prepared from learner-supplied details on November 8, 2026.*
