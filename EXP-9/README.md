# Ex. No 9: Identifying Suspicious Processes Using Process Explorer

---

## 📋 Overview
Process Explorer is an advanced process monitoring tool from Microsoft Sysinternals that provides deep visibility into the running state of a Windows system. Unlike the standard Task Manager, Process Explorer displays a hierarchical process tree, shows detailed DLL and handle information, verifies digital signatures, integrates with VirusTotal for malware scanning, and reveals hidden or disguised processes. These capabilities make it an indispensable tool for live forensic triage and malware detection on Windows systems.

---

## 🛠️ Experiment Objectives
1. Familiarize with the Process Explorer interface and its color-coded process categorization.
2. Identify potentially suspicious processes through behavioral analysis.
3. Verify digital signatures and inspect process image paths for anomalies.
4. Utilize the VirusTotal integration to cross-reference processes against malware databases.

---

## 🖥️ Software and Tools Required
- **Process Explorer** — Downloaded from Microsoft Sysinternals (`procexp64.exe`)
- **Windows operating system** (Windows 10/11)
- Administrator privileges for full process visibility

---

## Step 1: Launch Process Explorer and Examine the Process Tree

Run `procexp64.exe` as Administrator to obtain full visibility of all system processes. The main window displays a hierarchical tree view where child processes are nested under their parent processes.

| Process Tree | Nested Processes |
| :---: | :---: |
| ![1](1.png) | ![2](2.png) |
| *Figure 1.1: Examining the process tree.* | *Figure 1.2: Child processes.* |

### 🎨 Color-Coded Process Categories:
| Color | Meaning |
| :--- | :--- |
| **Light Blue** | Processes running under the current user account |
| **Dark Blue / Purple** | Services and system-level processes |
| **Pink** | Suspended processes |
| **Green** | Newly spawned processes (flash briefly) |
| **Red** | Processes that have just terminated |


---

## Step 2: Inspect Suspicious Process Properties

Right-click any suspicious process and select **Properties** to examine critical forensic indicators:

- **Image Path** — Legitimate system processes reside in `C:\Windows\System32\`. Executables running from `AppData\Local\Temp\`, user folders, or random directories are red flags.
- **Verified Signer** — Legitimate software from trusted vendors (Microsoft, Adobe, etc.) will have valid digital signatures. "Unable to verify" or missing signatures indicate potentially malicious binaries.
- **Parent Process** — Unexpected parent-child relationships (e.g., `svchost.exe` spawned by `explorer.exe` instead of `services.exe`) suggest process injection or masquerading.

| Suspicious Properties | Signature Verification |
| :---: | :---: |
| ![3](3.png) | ![4](4.png) |
| *Figure 2.1: Inspecting suspicious process properties.* | *Figure 2.2: Verifying image path and signatures.* |

---


## Step 3: VirusTotal Integration for Malware Detection

Process Explorer integrates directly with VirusTotal, allowing each running process to be submitted for scanning against 70+ antivirus engines. Enable this feature via **Options → VirusTotal.com → Check VirusTotal.com**.

The VirusTotal column displays detection ratios:
- **0/72** — Clean, no antivirus engines detected malware
- **23/72** — Critical alert: 23 out of 72 engines flagged this process as malicious

| VirusTotal Scan | Detection Results |
| :---: | :---: |
| ![5](5.png) | ![6](6.png) |
| *Figure 3.1: VirusTotal integration.* | *Figure 3.2: Detection ratios.* |

---


## 🔍 Key Indicators of Suspicious Processes

| Indicator | Clean Process | Suspicious Process |
| :--- | :--- | :--- |
| **Image Path** | `C:\Windows\System32\` | `C:\Users\*\AppData\Temp\` |
| **Digital Signature** | Valid, trusted publisher | Unable to verify / Missing |
| **Description** | Clear, descriptive name | Blank or generic |
| **Company Name** | Microsoft Corporation, etc. | Unknown / Blank |
| **CPU/Memory** | Normal resource usage | Abnormally high consumption |
| **VirusTotal** | 0/72 detections | Multiple detections |
| **Network Activity** | Expected connections | Unknown external IPs |

---

## Step 4: Remediation Actions

When a malicious process is confirmed:

1. **Kill Process** — Right-click → Kill Process to terminate immediately
2. **Suspend Process** — Right-click → Suspend if further analysis is needed before termination
3. **Locate Source** — Navigate to the file path and quarantine/delete the executable
4. **Full System Scan** — Run comprehensive antivirus and anti-malware scans (e.g., Windows Defender, Malwarebytes)

---

## ✅ Result
Process Explorer was successfully used to identify suspicious processes on a Windows system. The process tree analysis revealed anomalous behavior, the Properties inspection uncovered unsigned executables running from temporary directories, and the VirusTotal integration confirmed malware presence with a 23/72 detection ratio identifying ransomware variants. The identified processes were terminated and their source files quarantined for further forensic analysis.

---
