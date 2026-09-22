# Ex. No 6: Disk Forensics Using The Sleuth Kit (TSK)

**Course / Lab:** Digital Forensics Laboratory  
**Experiment:** Disk Forensics Using The Sleuth Kit (TSK)  
**Candidate Name:** Sanjeevi Kumar S  
**Date:** September 22, 2026  

---

## 📋 Overview
The Sleuth Kit (TSK) is a collection of powerful command-line tools for forensic analysis of disk images and file systems. It enables investigators to examine partition layouts, analyze file system structures, list both active and deleted files, and recover deleted evidence — all while maintaining forensic integrity. TSK supports NTFS, FAT, EXT, HFS+, and other file system types commonly encountered during investigations.

---

## 🛠️ Experiment Objectives
1. Analyze the partition layout of a forensic disk image using `mmls`.
2. Examine file system metadata and structural details using `fsstat`.
3. List all files (including deleted entries) within a partition using `fls`.
4. Recover a deleted file from the disk image using `icat` and verify its integrity.

---

## 🖥️ Software and Tools Required
- **The Sleuth Kit (TSK)** — Pre-installed on most forensic Linux distributions
- A sample disk image file (`.dd`, `.raw`, `.img`, or `.E01`)
- **Linux environment** (e.g., Ubuntu, Kali Linux)

---

## Step 1: Analyze the Partition Layout with `mmls`

The `mmls` command displays the partition table of a disk image, showing the start sector, end sector, length, and type of each partition. This is the first step in any disk forensic investigation.

```bash
analyst@forensics:~$ mmls disk_image.dd
```

![Partition Layout Analysis](01_mmls_partition_layout.jpg)
*Figure 6.1: The `mmls` output reveals the DOS partition table structure, identifying NTFS, Linux, and Swap partitions along with unallocated regions.*

---

## Step 2: Examine File System Details with `fsstat`

Using the partition offset obtained from `mmls`, we inspect the target file system's metadata. The `fsstat` command provides critical information including file system type, volume serial number, cluster size, sector size, and MFT details.

```bash
analyst@forensics:~$ fsstat -o 63 disk_image.dd
```

![File System Statistics](02_fsstat_filesystem_info.jpg)
*Figure 6.2: The `fsstat` output confirms an NTFS file system with 4096-byte clusters, 512-byte sectors, and detailed MFT metadata including total and free entries.*

---

## Step 3: List Files (Including Deleted) with `fls`

The `fls` command recursively lists all files and directories within the specified partition. Deleted files are marked with an asterisk (`*`), making them immediately identifiable for recovery.

```bash
analyst@forensics:~$ fls -o 63 -r disk_image.dd
```

![File Listing with Deleted Files](03_fls_file_listing.jpg)
*Figure 6.3: The `fls` output displays the file system contents. Entries prefixed with `*` (e.g., `deleted_evidence.doc`, `secret_notes.txt`) indicate deleted files available for recovery.*

---

## Step 4: Recover a Deleted File with `icat`

Using the inode number of the deleted file (obtained from `fls` output), the `icat` command extracts the raw file content and redirects it to a new file. The recovered file is then verified using the `file` command and an MD5 hash for integrity.

```bash
analyst@forensics:~$ icat -o 63 disk_image.dd 28 > recovered_file.doc
analyst@forensics:~$ file recovered_file.doc
analyst@forensics:~$ md5sum recovered_file.doc
```

![Deleted File Recovery](04_icat_file_recovery.jpg)
*Figure 6.4: The `icat` command successfully recovers the deleted file. The `file` command confirms it as a valid Microsoft Word document, and `md5sum` generates a cryptographic hash for chain-of-custody documentation.*

---

## 📊 Summary of TSK Commands Used

| Command | Purpose | Key Output |
| :--- | :--- | :--- |
| `mmls` | Display partition table layout | Partition offsets, types, sizes |
| `fsstat` | Show file system metadata | FS type, cluster/sector sizes, MFT info |
| `fls` | List files (including deleted) | File names, inode numbers, deletion status |
| `icat` | Extract file content by inode | Recovered file data stream |

---

## ✅ Result
Disk forensics was successfully performed using The Sleuth Kit tools. The partition layout was analyzed with `mmls`, file system structure was examined with `fsstat`, all files (including deleted ones marked with `*`) were listed using `fls`, and a deleted file was recovered intact using `icat` with its integrity verified via MD5 hashing.
