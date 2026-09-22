# Ex. No. 8: Steganography Detection Using StegExpose

**Course / Lab:** Digital Forensics Laboratory  
**Experiment:** Steganography Detection Using StegExpose  
**Status:** Procedure and analysis record

---

## Overview

Steganography conceals data inside an otherwise ordinary digital object. StegExpose is a Java-based detector focused on least-significant-bit steganography in lossless images. Its score is an investigative lead, not proof on its own: a flagged image should be preserved and assessed with additional methods before reaching a conclusion.

## Objectives

1. Preserve a controlled set of known-clean and known-stego test images.
2. Run StegExpose in batch and individual-image modes.
3. Record the score, command line, tool version, and file hash for each sample.
4. Triage high-scoring files for corroborating analysis.

## Tools Required

- StegExpose JAR
- Java Runtime Environment
- Controlled PNG or BMP samples
- Hashing utility such as `sha256sum` or `Get-FileHash`

## Step 1: Preserve and hash the sample set

Place only lab-approved samples in a case folder. Hash the source images before analysis and do not overwrite them with generated output.

```bash
sha256sum samples/* > sample-hashes.sha256
java -jar StegExpose.jar samples/
```

![StegExpose project reference](https://opengraph.githubassets.com/63631fb6d7fbb200560d8fd607115b5a7961fc6b4ef72f6287a174c0f334534d/b3dk7/StegExpose)

*Figure 8.1: The maintained StegExpose project reference. The tool combines several statistical techniques for LSB-steganography triage.*

## Step 2: Record and interpret suspect scores

Capture the raw terminal output to a text file and enter the sample name, SHA-256 value, score, threshold, and analyst decision in the worksheet. Do not label a file malicious or steganographic solely because one score exceeds a threshold.

| Score range | Triage decision | Next action |
| --- | --- | --- |
| Below the local baseline | Low priority | Retain the log and move to the next sample |
| Near the chosen threshold | Review | Compare to clean control images and inspect metadata |
| Clearly above the chosen threshold | Escalate | Preserve the file and use independent corroborating methods |

## Step 3: Perform corroborating checks

For a flagged sample, examine metadata, dimensions, colour depth, and file format. Compare it with a known-clean image from the same source where possible. Use an additional steganalysis method or controlled extraction test only within the authorised lab scenario.

```bash
java -jar StegExpose.jar samples/suspect.png
exiftool samples/suspect.png
```

## Result

The procedure produces a reproducible triage record: each score is tied to a particular hashed source file, command, threshold, and follow-up decision. Statistical output is documented as an indicator requiring corroboration, not as conclusive proof.

## Visual source

Figure 8.1 uses the public project preview from the [StegExpose repository](https://github.com/b3dk7/StegExpose). It identifies the genuine tool used in the procedure; it is not presented as a lab result screenshot.
