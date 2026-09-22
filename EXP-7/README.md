# Ex. No. 7: Android Logical Acquisition Using AFLogical OSE

**Course / Lab:** Digital Forensics Laboratory  
**Experiment:** Android Logical Acquisition Using AFLogical OSE  
**Status:** Procedure and analysis record

---

## Overview

AFLogical OSE performs logical acquisition from Android content providers. It can collect structured artifacts such as contacts, call logs, SMS/MMS records, and device information. Because a logical acquisition is not a physical image, the report must identify what was selected, what was collected, and any data unavailable through the operating-system interface.

## Objectives

1. Confirm an authorised Android test device is visible through ADB.
2. Install AFLogical OSE and select relevant data providers.
3. Capture logical data without altering the original export.
4. Transfer the export to the workstation and validate the received files.

## Tools Required

- AFLogical OSE APK
- Android Debug Bridge (ADB)
- An authorised Android device or emulator with USB debugging enabled
- An isolated forensic workstation

## Step 1: Verify the device and install the acquisition utility

Enable USB debugging only on an authorised device. Confirm the device serial returned by ADB, then record it in the acquisition notes.

```text
adb devices
adb install aflogical-ose.apk
```

![AFLogical OSE logical acquisition interface and ADB terminal](https://www.infosecinstitute.com/globalassets/wpcontentmedia/031616_1042_androidfore23.webp)

*Figure 7.1: A real AFLogical OSE interface alongside the ADB workflow. The selected providers determine the scope of the logical acquisition.*

## Step 2: Select providers and capture data

Open AFLogical OSE on the device. Select only the data types authorised by the lab scenario, such as Contacts, Call Log, SMS/MMS, and Device Information, then start the capture. Note the tool version, device state, date/time settings, and selected providers.

## Step 3: Transfer the extraction to the workstation

Export the acquisition directory to a case-specific folder. Do not edit the original extraction. Create a separate working copy for spreadsheet review or parsing.

```text
adb pull /sdcard/forensics/ C:\Forensic_Cases\Case001\logical-acquisition\
Get-FileHash C:\Forensic_Cases\Case001\logical-acquisition\* -Algorithm SHA256
```

![AFLogical OSE data pulled from an Android device](https://www.infosecinstitute.com/globalassets/wpcontentmedia/031616_1042_androidfore25.webp)

*Figure 7.2: A live logical-acquisition transfer showing CSV and XML artifacts being copied to the forensic workstation.*

## Data Categories

| Category | Typical export | Example fields to review |
| --- | --- | --- |
| Contacts | CSV | Name, number, email, account type |
| Call logs | CSV | Number, direction, duration, timestamp |
| SMS/MMS | CSV | Address, message body, timestamp, read state |
| Device information | XML or CSV | Model, OS version, device identifiers |

## Evidence Handling Notes

- Keep the original device connected only for the shortest necessary period.
- Preserve the unmodified acquisition folder and record hashes for each exported file.
- Use local time, time zone, tool version, and device serial in the chain-of-custody note.
- Treat absent records as limitations of logical acquisition rather than proof that no data existed.

## Result

The workflow produces a structured, hashable logical export suitable for review while clearly documenting collection scope and limitations.

## Visual source

Figures 7.1 and 7.2 are independently published AFLogical OSE acquisition captures from [Infosec's Android logical acquisition guide](https://www.infosecinstitute.com/resources/digital-forensics/android-forensic-logical-acquisition/). They are tool-interface references, not evidence from a lab device.
