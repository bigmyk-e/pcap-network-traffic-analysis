# 🔍 PCAP Network Traffic Analysis — Lumma Stealer Detection

**Date:** May 2026
**Skills:** Wireshark · tcpdump · Network Forensics · OSINT · 
Threat Intelligence · FTP Analysis · Credential Recovery

---

## Scenario

A SOC alert was triggered at Astley Financial after an endpoint 
began exhibiting abnormal network behaviour — multiple detections 
pointing to a potential info-stealer malware variant. As the 
analyst on duty, I was tasked with analysing the captured network 
traffic to identify the threat, scope the compromise, and document 
findings.

**Evidence file:** tcpdump_challenge.pcap  
**Total packets:** 1344

---

## Methodology

Opened the PCAP in Wireshark and used targeted tcpdump filters 
to work through the traffic systematically:

- Protocol hierarchy analysis to understand traffic distribution
- ICMP filter to identify external ping targets and ASN ownership
- HTTP stream inspection to extract POST payloads and headers
- FTP session analysis to recover authentication and file activity
- OSINT on extracted User-Agent string for malware identification

---

## Key Findings

| Finding | Detail |
|---|---|
| ICMP Ping Destination | 149.154.167.99 |
| ASN | AS13335 (Cloudflare) |
| HTTP POST Requests | 1 |
| Password Exfiltrated | Recovered in plaintext via HTTP POST |
| Secondary Protocol | FTP (Port 21) |
| FTP Credentials | Recovered from session |
| File Retrieved | readme.txt |
| Malware Identified | Lumma Stealer |
| C2 URL (defanged) | hxxps[://]t[.]me/+zz0192lskaaa |

---

## Malware Identification

The HTTP requests contained a non-standard User-Agent string — 
TeslaBrowser/5.5. This string does not match any legitimate 
browser or update agent. OSINT lookup confirmed this User-Agent 
is associated with Lumma Stealer, a well-documented info-stealer 
known for credential harvesting and Telegram-based C2 exfiltration.

---

## Attack Chain

1. Endpoint performs ICMP ping to external IP — connectivity check
2. Credentials harvested and exfiltrated via plaintext HTTP POST
3. Malware authenticates to FTP server using valid credentials
4. File retrieved from file sharing server
5. Endpoint attempts C2 connection via Telegram URL

---

## Tools Used

| Tool | Purpose |
|---|---|
| Wireshark | Packet inspection, stream following, filter analysis |
| tcpdump | Command-line packet filtering and counting |
| ipinfo.io | ASN lookup on external IP |
| OSINT | User-Agent malware identification |

---

## Full Report

→ [View Full Analysis Report (PDF)](SOC-Challenge-PCAP-Analysis.pdf)
