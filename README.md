# Nmap Network Reconnaissance & Service Exposure Assessment

> **Proxmox-Based Network Reconnaissance & Security Assessment Laboratory**

A hands-on cybersecurity laboratory project demonstrating authorized network reconnaissance, service/version enumeration, OS fingerprinting, service validation, and evidence-based service exposure assessment using **Nmap**.

This project was developed as a practical cybersecurity portfolio project focused on skills relevant to **Network Security, SOC, and Blue Team activities**.

---

## Overview

This project documents a structured network reconnaissance and service exposure assessment performed within a **school-provided Proxmox laboratory environment**.

The assessment used:

- **Kali Linux** as the security assessment and Nmap scanning host
- **Ubuntu Server** as Target 1
- **Debian 13 Trixie** as Target 2
- **Nmap 7.95** for network reconnaissance and service enumeration
- **cURL** for HTTP service validation

The project demonstrates how reconnaissance results can be collected, validated, analyzed, and documented without automatically treating exposed services as vulnerabilities.

---

## Objectives

The project objectives were to:

- Perform authorized network discovery
- Identify reachable laboratory targets
- Enumerate exposed services and software versions
- Attempt automated OS identification
- Validate identified services using additional evidence
- Assess security relevance of exposed network services
- Capture reproducible evidence for each major assessment phase
- Compare service exposure between two Linux targets
- Produce a technical assessment report suitable for cybersecurity portfolio use
- Document limitations and authorization boundaries

---

## Lab Environment

The assessment was conducted using a school-provided Proxmox environment.

| System | Operating System | IP Address | Role |
|---|---|---|---|
| Assessment VM | Kali Linux | `192.168.1.139` | Nmap scanning and assessment |
| Target 1 | Ubuntu Server | `192.168.1.120` | Authorized assessment target |
| Target 2 | Debian 13 Trixie | `192.168.1.141` | Authorized assessment target |

### Network Environment

- Proxmox network: `vmbr209801`
- Laboratory subnet: `192.168.1.0/24`
- Network infrastructure was provided and managed by the school
- Internet access was available through the school-managed network infrastructure
- No shared infrastructure, bridge configuration, or physical networking components were modified

Only the specifically assigned laboratory targets were intentionally assessed.

---

## Assessment Methodology

The assessment followed a structured reconnaissance workflow:

### 1. Laboratory Preparation

Configured the authorized virtual machines within the school-provided Proxmox environment.

### 2. Network Verification

Verified addressing and connectivity between the Kali assessment VM and the authorized targets.

### 3. Host Discovery

Used Nmap host discovery to confirm target reachability.

```bash
nmap -sn 192.168.1.120
nmap -sn 192.168.1.141
```

### 4. Service & Version Enumeration

Identified exposed services and software versions.

```bash
nmap -sV -p 8000 192.168.1.120
nmap -sV 192.168.1.141
```

### 5. OS Fingerprinting

Attempted automated operating system identification.

```bash
sudo nmap -O 192.168.1.120
sudo nmap -O 192.168.1.141
```

### 6. Service Validation

Validated the HTTP service identified on Target 1.

```bash
curl -I http://192.168.1.120:8000
```

### 7. Findings Analysis

Reviewed reconnaissance and validation results and documented observations supported by collected evidence.

### 8. Comparative Assessment

Compared the network-facing services identified on the Ubuntu and Debian targets.

---

## Key Results

### Target 1 — Ubuntu Server

**IP:** `192.168.1.120`

| Port | Service | Version |
|---|---|---|
| `8000/tcp` | HTTP | SimpleHTTPServer 0.6 / Python 3.12.3 |

The HTTP service was intentionally enabled within the laboratory for service enumeration and validation.

cURL validation returned:

```text
HTTP/1.0 200 OK
Server: SimpleHTTP/0.6 Python/3.12.3
```

### Target 2 — Debian 13 Trixie

**IP:** `192.168.1.141`

| Port | Service | Version |
|---|---|---|
| `22/tcp` | SSH | OpenSSH 10.0p2 Debian 7+deb13u4 |

### OS Detection

Nmap OS fingerprinting did **not** produce exact operating system matches for either target.

The actual operating systems were known from the laboratory configuration, so the Nmap results were treated as **inconclusive** rather than definitive.

---

## Security Findings

### F-01 — Temporary HTTP Service Exposure on TCP/8000

Nmap identified an actively responding HTTP service on the Ubuntu target.

The service contributed to the target's reachable network attack surface. However, because it was intentionally enabled for laboratory assessment, the observation **does not by itself establish a vulnerability or exploitability**.

**Recommendation:** Disable the temporary HTTP service after testing and verify that TCP/8000 is no longer exposed.

### Target 2 — SSH Service Exposure on TCP/22

The Debian target exposed SSH on TCP/22 using OpenSSH 10.0p2.

SSH represents a network-accessible administrative service and therefore contributes to the target's exposed service surface.

**Recommendation:** Confirm that SSH access is required and restrict access appropriately where applicable.

---

## Important Assessment Principle

> **An exposed service is not automatically a vulnerability.**

This project intentionally distinguishes between:

- Observable service exposure
- Service identification and version information
- Validation of service behavior
- Confirmed vulnerabilities or exploitability

No vulnerability was declared solely because a port was open.

---

## Repository Structure

```text
Nmap-Network-Reconnaissance-Lab/
├── README.md
├── documentation/
│   └── Nmap_Network_Reconnaissance_Laboratory_Portfolio_Project.pdf
├── diagrams/
│   └── lab-architecture.png
├── evidence/
│   ├── 01-proxmox-target-vm/
│   ├── 02-security-vm/
│   ├── 03-connectivity/
│   ├── 04-network-boundary/
│   ├── 05-host-discovery/
│   ├── 06-service-enumeration/
│   ├── 07-os-identification/
│   ├── 08-service-validation/
│   ├── 09-second-target/
│   ├── 10-target2-host-discovery/
│   ├── 11-target2-service-enumeration/
│   └── 12-target2-os-identification/
├── results/
│   ├── target1-service-enumeration.md
│   ├── target1-os-detection.md
│   ├── target2-service-enumeration.md
│   └── target2-os-detection.md
└── reports/
    └── technical-assessment-report.md
```

---

## Results Documentation

Detailed Markdown results are available for each major Nmap assessment activity:

- [Target 1 — Service & Version Enumeration](results/target1-service-enumeration.md)
- [Target 1 — OS Detection](results/target1-os-detection.md)
- [Target 2 — Service & Version Enumeration](results/target2-service-enumeration.md)
- [Target 2 — OS Detection](results/target2-os-detection.md)

---

## Technical Report

The complete technical assessment report documents the:

- Laboratory environment
- Assessment scope
- Methodology
- Reconnaissance results
- Security findings
- Target comparison
- Recommendations
- Limitations
- Final assessment conclusion

[View the Technical Assessment Report](reports/technical-assessment-report.md)

---

## Evidence

The project contains **12 documented evidence items** covering:

1. Proxmox target VM
2. Security assessment VM
3. Connectivity verification
4. Network boundary
5. Target 1 host discovery
6. Target 1 service enumeration
7. Target 1 OS identification
8. Target 1 service validation
9. Second target configuration
10. Target 2 host discovery
11. Target 2 service enumeration
12. Target 2 OS identification

The evidence was prepared for portfolio presentation with unnecessary identifiers such as MAC addresses and school/account-specific information removed where appropriate.

---

## Tools & Technologies

| Tool / Technology | Purpose |
|---|---|
| Proxmox VE | Virtual laboratory infrastructure |
| Kali Linux | Security assessment host |
| Nmap 7.95 | Network reconnaissance and service enumeration |
| Ubuntu Server | Target 1 |
| Debian 13 Trixie | Target 2 |
| Python SimpleHTTPServer | Intentionally enabled HTTP service for Target 1 testing |
| OpenSSH | SSH service on Target 2 |
| cURL | HTTP service validation |

---

## Limitations

This assessment focused on reconnaissance, service exposure, and validation.

The following activities were **not performed**:

- Exploitation of identified services
- Credential attacks
- Password cracking
- Unauthorized access attempts
- Scanning of external systems
- Scanning of unrelated systems within the shared environment
- Full vulnerability assessment of the target operating systems
- Production network testing

OS fingerprinting was inconclusive for both targets.

---

## Authorization & Safety Boundary

All technical activities documented in this repository were performed against intentionally configured virtual machines within an authorized laboratory environment for cybersecurity learning and portfolio development.

The assessment was limited to:

- `192.168.1.120` — Ubuntu Server
- `192.168.1.141` — Debian 13 Trixie

The broader shared Proxmox network was not intentionally scanned.

No shared infrastructure was modified as part of the project.

**Do not use the commands or methodology documented here against systems you do not own or do not have explicit authorization to assess.**

---

## Portfolio Value

This project demonstrates practical experience with:

- Network reconnaissance
- Nmap host discovery
- Service and version enumeration
- OS fingerprinting
- Service validation
- Evidence collection
- Security-focused analysis
- Risk-aware reporting
- Technical documentation
- Authorized security assessment practices

These activities support foundational skills relevant to **SOC Analyst, Blue Team, Network Security, and Cybersecurity Analyst** roles.

---

## Author

**Moises Ceazar C. Del Mundo**  
BSIT – Information Security  
De La Salle Lipa

---

## Project Status

**Completed — October 2026**

This repository represents a completed authorized cybersecurity laboratory assessment with documented evidence, results, and technical reporting.
