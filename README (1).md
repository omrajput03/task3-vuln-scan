# Task 3 — Basic Vulnerability Scan on Local Machine

**ElevateLabs Cyber Security Internship**

## Overview

Performed a full-port vulnerability scan on localhost using **Nmap 7.95** with NSE (Nmap Scripting Engine) vulnerability scripts on Kali Linux. This task demonstrates introductory vulnerability assessment skills including scanning, CVE identification, risk rating, and remediation planning.

## Tool Used

- **Nmap 7.95** with `--script vuln` (free, industry-standard, pre-installed on Kali Linux)
- Alternative tools suggested by task: OpenVAS, Nessus Essentials

## Scan Command

```bash
nmap -sV -sC --script vuln -p- localhost
```

| Flag | Purpose |
|------|---------|
| `-sV` | Detect service versions |
| `-sC` | Run default NSE scripts |
| `--script vuln` | Run all vulnerability detection scripts |
| `-p-` | Scan all 65,535 TCP ports |

## Results Summary

| Finding | Detail |
|---------|--------|
| Open Ports | 1 (port 38861) |
| Service | Golang net/http server |
| Vulnerability Found | CVE-2007-6750 (Slowloris DoS) |
| Severity | Medium |
| XSS/CSRF | Not Found |

## Key Finding: Slowloris (CVE-2007-6750)

The Go HTTP server running on port 38861 was found **likely vulnerable** to the Slowloris Denial-of-Service attack due to missing connection read timeouts.

**Fix:** Add `ReadTimeout` and `ReadHeaderTimeout` to the Go `http.Server` config.

## Files in This Repo

| File | Description |
|------|-------------|
| `vulnerability_report.md` | Full vulnerability report with CVE details, risk assessment, and remediation |
| `scan_output.txt` | Raw Nmap terminal output |
| `screenshots/` | Screenshots of scan in progress and results |
| `README.md` | This file |

## What I Learned

- How Nmap NSE scripts work for vulnerability detection
- The Slowloris attack mechanism and why stateless connection limits matter
- How to read and interpret CVE entries
- CVSS scoring and how to prioritize vulnerabilities by context, not just score
- The difference between "likely vulnerable" (scanner heuristic) vs confirmed exploitation

## Interview Q&A

See full answers in `vulnerability_report.md` — covers all 8 interview questions from the task brief.
