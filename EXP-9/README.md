# Ex. No. 9: Suspicious Process Triage Using Process Explorer

**Course / Lab:** Digital Forensics Laboratory  
**Experiment:** Suspicious Process Triage Using Process Explorer  
**Status:** Procedure and analysis record

---

## Overview

Process Explorer is a Microsoft Sysinternals utility that exposes a running Windows process tree, loaded DLLs, handles, image paths, digital-signature information, and VirusTotal lookups. This lab uses a controlled system to distinguish investigation indicators from conclusions: an unusual name or high CPU use merits inspection, but is not by itself malware proof.

## Objectives

1. Examine the live process tree and parent-child relationships.
2. Review a selected process's image path, publisher, command line, and signature state.
3. Use VirusTotal integration only under the lab's data-handling rules.
4. Capture triage observations and preserve any specimen before remediation.

## Tools Required

- [Process Explorer](https://learn.microsoft.com/sysinternals/downloads/process-explorer)
- A Windows 10 or Windows 11 lab virtual machine
- Administrator privileges where permitted
- Internet access only if VirusTotal lookup has been approved

## Step 1: Inspect the process tree

Launch Process Explorer as Administrator in the lab VM. Expand the tree rather than relying only on process names. Record the process ID, parent process, launch time, user context, and resource usage for any item selected for review.

![Real Process Explorer interface showing hierarchical processes](https://s.yimg.com/ny/api/res/1.2/XFRN6fdAfTkZ6eJFd6QMRA--/YXBwaWQ9aGlnaGxhbmRlcjt3PTk2MDtoPTcyMg--/https%3A/media.zenfs.com/en/how_to_geek_999/fde13ef064724e3cb16cfe1c715cb0a7)

*Figure 9.1: A real Process Explorer view with process hierarchy, PID, CPU, memory, and publisher columns.*

## Step 2: Review process properties

Open **Properties** for the selected process and document the following indicators:

| Indicator | Typical benign pattern | Reason to investigate |
| --- | --- | --- |
| Image path | Expected application or system location | Temporary, unexpected, or user-writable directory |
| Verified signer | Valid publisher matching the executable | Missing, invalid, or unexpected publisher |
| Parent process | Consistent with normal launch chain | Unusual parent-child relationship |
| Command line | Expected switches and location | Obfuscated arguments or unexpected script host |
| Network activity | Expected destination and port | Unknown or unexplained external endpoint |

## Step 3: Use VirusTotal carefully

Enable **Options → VirusTotal.com → Check VirusTotal.com** only if policy permits an external hash lookup. Record the scan ratio and timestamp, but do not upload a sensitive binary without authorisation. A detection ratio is one lead among several; validate it against the path, signature, behaviour, and local security logs.

## Step 4: Preserve before remediating

If the lab scenario identifies a process as malicious, first document the PID, hash, image path, process tree, and relevant handles or network connections. Follow the incident procedure for memory capture, containment, and remediation; do not delete a suspected specimen before preserving the required evidence.

## Result

The triage workflow converts a live process observation into documented indicators that can be verified by signatures, hashes, parentage, and other evidence sources before a remediation decision is made.

## Visual source

Figure 9.1 is an independently published Process Explorer screenshot from [How-To Geek](https://tech.yahoo.com/computing/articles/4-free-tools-keep-usb-140015908.html). It is a tool-interface reference, not evidence from the lab VM.
