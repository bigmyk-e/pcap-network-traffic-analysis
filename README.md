# 🔍 PCAP Network Traffic Analysis — Lumma Stealer Detection

**Date:** May 2026  
**Skills:** Wireshark · tcpdump · Network Forensics · OSINT · Threat Intelligence · FTP Analysis

## Overview
Analysed a packet capture from a simulated SOC alert at Astley Financial. 
The endpoint was flagging abnormal behaviour consistent with info-stealer 
malware activity.

## Key Findings
- Identified **Lumma Stealer** via unique User-Agent string (TeslaBrowser/5.5)
- Recovered credential exfiltrated in plaintext via HTTP POST
- Extracted valid FTP credentials used to retrieve a file from the server
- Confirmed C2 communication over Telegram
- ASN lookup confirmed external connectivity checks pre-exfiltration

## Tools Used
Wireshark · tcpdump · ipinfo.io

## Report
→ [View Full Analysis (PDF)](./Lumma-Stealer-PCAP-Analysis.pdf)
