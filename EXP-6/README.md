# Ex. No. 6: Disk Forensics Using The Sleuth Kit

**Course / Lab:** Digital Forensics Laboratory  
**Experiment:** Disk Forensics Using The Sleuth Kit  
**Status:** Procedure and analysis record

---

## Overview

The Sleuth Kit (TSK) is a command-line framework for examining forensic disk images and file systems. This experiment records a defensible workflow: identify the partition layout first, use the correct sector offset to inspect the file system, enumerate active and deleted entries, then recover a selected inode without modifying the source image.

## Objectives

1. Identify partitions and their starting sectors with `mmls`.
2. Inspect file-system metadata with `fsstat`.
3. List active and deleted entries with `fls`.
4. Extract a selected file by metadata address with `icat` and record a hash.

## Tools Required

- The Sleuth Kit
- A read-only forensic image such as `.dd`, `.raw`, `.img`, or `.E01`
- A Linux forensic workstation or isolated virtual machine

## Step 1: Identify the partition layout

Work from a verified copy of the evidence image. The `mmls` output supplies the partition start sector used by subsequent commands.

```bash
mmls evidence-image.dd
```

![Live TSK terminal showing mmls and fls output](https://halilozturkci.com/_next/image?q=75&url=%2Fimages%2Fcanli-sistemler-uzerinde-the-sleuth-kit-tsk-araclari-ile-adl%2F1766548008-tsk_linux_mmls_fls.png&w=1920)

*Figure 6.1: A live TSK terminal session showing partition identification and file listing. Record the relevant partition's start sector before moving on.*

## Step 2: Inspect the selected file system

Replace `2048` with the sector offset obtained in Step 1. The command reports the file-system type, allocation details, block and cluster sizing, and metadata structures.

```bash
fsstat -o 2048 evidence-image.dd
```

Record the image name, hash, selected partition, offset, analyst, and acquisition time in the case notes. These details make the later listing and recovery reproducible.

## Step 3: Enumerate files and deleted entries

Use recursive listing to locate candidate evidence. In TSK output, entries marked with `*` are deleted. Preserve the metadata address/inode of every item selected for recovery.

```bash
fls -o 2048 -r evidence-image.dd
```

## Step 4: Recover and verify a file

Use the metadata address shown by `fls`; the value `12345` below is a placeholder, not a finding. Hash the recovered output and keep the hash with the recovery log.

```bash
icat -o 2048 evidence-image.dd 12345 > recovered-file.bin
file recovered-file.bin
sha256sum recovered-file.bin
```

## Commands Used

| Command | Purpose | Evidence recorded |
| --- | --- | --- |
| `mmls` | Displays partition layout | Partition type and start sector |
| `fsstat` | Reports file-system structure | File-system type and allocation details |
| `fls` | Lists directory entries | Paths, deletion markers, metadata addresses |
| `icat` | Extracts content by metadata address | Recovered file and its SHA-256 hash |

## Result

The documented workflow preserves the original disk image while establishing the partition offset, file-system characteristics, directory entries, and a repeatable recovery path for a selected deleted file.

## Visual source

Figure 6.1 is an independently published live TSK terminal capture from [Halil Ozturkci's TSK walkthrough](https://halilozturkci.com/post/canli-sistemler-uzerinde-the-sleuth-kit-tsk-araclari-ile-adli-bilisim-incelemesi). It is used as a tool-interface reference and is not case evidence.
