# Ex. No 1: Evidence Acquisition Using AccessData FTK Imager

**Course / Lab:** Digital Forensics Laboratory  
**Experiment:** Evidence Acquisition Using AccessData FTK Imager[cite: 2]  
**Date:** August 27, 2026  

---

## 📋 Overview
Forensic Toolkit (FTK) Imager is a widely used computer forensics software product designed for acquiring and analyzing digital evidence[cite: 2]. To maintain the integrity of evidence during investigations, FTK Imager provides reliable methods for capturing both volatile and non-volatile memory without altering the original source files[cite: 2, 3].

---

## 🛠️ Experiment Objectives
1. Acquire volatile memory (RAM) along with pagefile data from a live system.
2. Acquire non-volatile memory (disk images or specific logical partitions) using safe acquisition workflows.
3. Verify evidence integrity using cryptographic hash values (MD5 and SHA1)[cite: 3].

---

## Part 1: Acquiring Volatile Memory (RAM)

Volatile memory contains active processes, network connections, and temporary data that disappear when a system is powered off.

### Steps:
1. Launch **AccessData FTK Imager** and click on the **Capture Memory** icon on the toolbar[cite: 3].
2. Choose your **Destination path** and enter a filename for the memory dump (e.g., `memdump.mem`)[cite: 3].
3. Check the options to **Include pagefile** (to capture `pagefile.sys` data from the C drive) and **Create AD1 file** if required[cite: 3].
4. Click **Capture Memory** to begin the process and wait for completion[cite: 3].

![Capture Memory Toolbar](docs/assets/ftk-step1-memory-icon.png)  
*Figure 1: Navigating to the volatile memory capture icon.*

![Memory Progress](docs/assets/ftk-step2-memory-progress.png)  
*Figure 2: Memory capture progress and completion.*

---

## Part 2: Acquiring Non-Volatile Memory (Logical Drive / Partition)

To save storage space and time during laboratory workflows, investigators can choose to acquire a single logical partition rather than an entire physical hard drive[cite: 3].

### Steps:
1. Open FTK Imager and click on the **Create Disk Image** icon[cite: 3].
2. Select **Logical Drive** as the source evidence type and pick your target partition (e.g., `D:` or `E:`)[cite: 3].
3. Fill in the **Evidence Item Information** (Case Number, Evidence Number, Unique Description, Examiner, and Notes)[cite: 3].
4. Set your **Image Destination folder**, filename, and set the **Image Fragment Size** to `0` for a single unified file[cite: 3].
5. Check **Verify images after they are created** to automatically calculate and verify checksums[cite: 3].
6. Click **Start** to initiate the acquisition[cite: 3].

![Create Disk Image Source](docs/assets/ftk-step3-select-source.png)  
*Figure 3: Selecting source evidence type (Logical Drive).*

![Image Destination](docs/assets/ftk-step4-destination.png)  
*Figure 4: Configuring destination path and verification settings.*

---

## 🔍 Verification & Cryptographic Hashes

To ensure that the acquired evidence has not been tampered with or corrupted, FTK Imager automatically computes cryptographic hashes upon completion[cite: 3].

```text
Image Type: Raw (dd)
Source data size: 9968 MB
Sector count: 2041446

[Computed Hashes]
MD5 checksum:    043d83c157ac850bcf03e0285932fbf1
SHA1 checksum:   12713a645e6bbd0baebf9af9e3634fb11a559641

Image Verification Results:
MD5 checksum:    043d83c157ac850bcf03e0285932fbf1 : verified
SHA1 checksum:   12713a645e6bbd0baebf9af9e3634fb11a559641 : verified
