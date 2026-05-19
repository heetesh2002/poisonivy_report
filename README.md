# Poison Ivy (PIVY)

**Report Date:** May 2026 | **Malware Type:** Remote Access Trojan (RAT)

---

## Overview

Poison Ivy is a Windows-based RAT first identified in **2005**. Its point-and-click builder made it accessible to operators of all skill levels, leading to widespread adoption by nation-state APT groups, cybercriminals, and hacktivists. Despite its age, variants remain in active circulation as of 2026.

---

## Key Facts

| Field | Detail |
|---|---|
| **Aliases** | PIVY, PoisonIvy RAT, Backdoor:W32/PoisonIvy |
| **First Seen** | 2005 |
| **Platform** | Microsoft Windows (all versions) |
| **Encryption** | Camellia-256 (key derived from operator password) |
| **Default C2 Port** | TCP 3460 (configurable) |
| **Primary Use** | Espionage, credential theft, data exfiltration |
| **Status** | Active — variants still in circulation |

---

## Core Capabilities

- Keylogging & screen/video capture
- Remote shell access & file management
- Password and credential harvesting
- Process & registry manipulation
- Webcam & microphone surveillance
- DLL injection into system processes
- Plugin-based capability extension

---

## Associated Threat Actors

| Actor | Nexus | Targets | Notable |
|---|---|---|---|
| **admin@338** | China | Finance, Govt, Defense | Active since Jan 2008 |
| **th3bug** | China | Education, Healthcare | Watering-hole specialist |
| **menuPass (APT10)** | China | Defense Contractors | DOJ-indicted: Zhu Hua & Zhang Shilong |
| **Nitro Campaign** | China | Govt, Chemical Mfg | Integrated Java zero-day (2012) |
| **Molerats** | Middle East | Israeli Govt | Used fake Microsoft certificate |
| **TA428** | China | East Asian Govt | Shared C2 with Cotx RAT |

---

## Key IOCs

- **IPs:** 219.76.208.163
- **Domains:** webserver.dynssl.com, webserver.freetcp.com, microsofta.byinter.net
- **MD5s:** 8010cae3e8431bb11ed6dc9acabb93b7, 0323de551aa10ca6221368c4a73732e6
- **Mutex:** Variable (148 unique mutexes documented across campaigns)
- **Passwords/Keys:** admin, admin@338, th3bug, menuPass

---

## MITRE ATT&CK Highlights

`T1566` Spearphishing · `T1189` Drive-By Compromise · `T1055` Process Injection  
`T1547.001` Registry Run Keys · `T1056.001` Keylogging · `T1219` Remote Access  
`T1003` Credential Dumping · `T1113` Screen Capture · `T1041` Exfil over C2

---

## Detection Guidance

- **YARA:** Target `$camellia$` string and Camellia-256 encrypted C2 traffic
- **Network:** Monitor unusual outbound TCP (default port 3460); decode with FireEye Calamine
- **Registry:** Check `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` for rogue entries
- **Forensics:** Scan NTFS Alternate Data Streams; inspect svchost.exe for injected DLLs
- **Tools:** FireEye Calamine (ChopShop + PyCommand) for memory & traffic decoding

---

## Evolution Timeline

| Year | Key Change |
|---|---|
| 2005 | First public identification; builder kit released |
| 2011–12 | Zero-day delivery (Flash, Java) adopted by Nitro / RSA campaigns |
| 2013 | Watering-hole pivot (th3bug); certificate abuse (Molerats) |
| 2017 | AppLocker bypass via Regsvr32 + fileless execution |
| 2019+ | TA428 reuses PIVY alongside custom Cotx RAT |
| 2020–26 | Commodity variants wrapped in updated packers continue circulating |

---

## Primary References

- FireEye (2013) — *Poison Ivy: Assessing Damage and Extracting Intelligence*
- Proofpoint (2019) — *Operation LagTime IT*
- US DOJ (2018) — *US v. Zhu Hua, Case No. 18-cr-891 (S.D.N.Y.)*
- F-Secure — *Backdoor:W32/PoisonIvy*
- Huntress (2025) — *Poison Ivy Malware: Analysis, Detection, Removal*

---
