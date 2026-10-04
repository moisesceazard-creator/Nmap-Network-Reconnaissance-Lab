# Nmap Network Reconnaissance & Service Exposure Assessment

## Technical Assessment Report

**Author:** Moises Ceazar C. Del Mundo  
**Program:** BSIT – Information Security  
**Institution:** De La Salle Lipa  
**Assessment Type:** Authorized Cybersecurity Laboratory Assessment  
**Primary Tool:** Nmap 7.95

---

## Executive Summary

This laboratory project documents an authorized network reconnaissance and service exposure assessment conducted within a controlled Proxmox-based cybersecurity environment.

The assessment used a Kali Linux security VM as the Nmap scanning host and two intentionally created Linux virtual machines as authorized targets:

- Ubuntu Server — `192.168.1.120`
- Debian 13 Trixie — `192.168.1.141`

Nmap was used for host discovery, service and version enumeration, and OS fingerprinting. cURL was additionally used to validate the HTTP service identified on the Ubuntu Server target.

The assessment identified different service exposure profiles between the two targets. Ubuntu exposed an intentionally enabled HTTP service on TCP/8000, while Debian exposed SSH on TCP/22.

Automated OS fingerprinting did not produce exact operating system matches for either target. The results were therefore treated as inconclusive.

The assessment demonstrates authorized reconnaissance, evidence collection, service validation, and security-focused analysis without performing exploitation or unauthorized access.

---

## 1. Environment

The laboratory was implemented using a school-provided Proxmox environment containing an assessment VM and two intentionally created Linux target VMs.

| System | Operating System | IP Address | Role |
|---|---|---|---|
| Assessment VM | Kali Linux | `192.168.1.139` | Nmap scanning and assessment |
| Target 1 | Ubuntu Server | `192.168.1.120` | Authorized assessment target |
| Target 2 | Debian 13 Trixie | `192.168.1.141` | Authorized assessment target |

The Proxmox network infrastructure was provided by the school. No shared network infrastructure, bridge configuration, or physical networking components were modified as part of the assessment.

All scanning activities were restricted to the specifically assigned laboratory targets.

---

## 2. Scope

The assessment was limited to the following authorized laboratory systems:

- `192.168.1.120` — Ubuntu Server
- `192.168.1.141` — Debian 13 Trixie

The Kali Linux assessment VM used for scanning was:

- `192.168.1.139`

The broader shared Proxmox network was not intentionally scanned.

---

## 3. Methodology

The assessment followed a structured reconnaissance workflow.

### Phase 1 — Laboratory Preparation

Created and configured the authorized virtual machines within the school-provided Proxmox environment.

### Phase 2 — Network Verification

Verified IP addressing and connectivity between the assessment VM and the authorized targets.

### Phase 3 — Host Discovery

Used Nmap host discovery to confirm that each authorized target was reachable.

```bash
nmap -sn 192.168.1.120
nmap -sn 192.168.1.141
```

### Phase 4 — Service & Version Enumeration

Used Nmap service detection to identify exposed services and software versions.

```bash
nmap -sV -p 8000 192.168.1.120
nmap -sV 192.168.1.141
```

### Phase 5 — OS Fingerprinting

Used Nmap OS detection to attempt automated operating system identification.

```bash
sudo nmap -O 192.168.1.120
sudo nmap -O 192.168.1.141
```

### Phase 6 — Service Validation

Validated the HTTP service identified on Target 1 using cURL.

```bash
curl -I http://192.168.1.120:8000
```

The service returned HTTP `200 OK`, confirming that the detected HTTP service was actively responding.

### Phase 7 — Findings Analysis

Reviewed the collected reconnaissance and validation results and documented only observations supported by the captured evidence.

### Phase 8 — Comparative Assessment

Compared the service exposure of the Ubuntu and Debian targets to identify differences in their network-facing services.

---

## 4. Results

### Target 1 — Ubuntu Server

**IP Address:** `192.168.1.120`

| Port | State | Service | Version |
|---|---|---|---|
| `8000/tcp` | Open | HTTP | SimpleHTTPServer 0.6 / Python 3.12.3 |

The HTTP service was intentionally enabled within the laboratory for service enumeration and validation.

The service was subsequently validated using cURL and returned:

```text
HTTP/1.0 200 OK
Server: SimpleHTTP/0.6 Python/3.12.3
```

### Target 2 — Debian 13 Trixie

**IP Address:** `192.168.1.141`

| Port | State | Service | Version |
|---|---|---|---|
| `22/tcp` | Open | SSH | OpenSSH 10.0p2 Debian 7+deb13u4 |

Nmap identified the service as an SSH service running on Linux.

### OS Detection

Nmap OS detection did not produce an exact operating system match for either target.

The actual operating systems were known from the laboratory configuration, so the Nmap results were treated as inconclusive rather than definitive.

---

## 5. Findings

### F-01 — Temporary HTTP Service Exposure on TCP/8000

**Target:** Ubuntu Server — `192.168.1.120`

**Observation:**  
Nmap identified TCP/8000 as an open HTTP service running SimpleHTTPServer 0.6 on Python 3.12.3.

**Evidence:**  
Nmap service/version enumeration and cURL HTTP response validation.

**Security Relevance:**  
An actively responding network service contributes to the target's reachable network attack surface.

The service was intentionally enabled within the laboratory for controlled assessment and therefore does not by itself demonstrate a vulnerability.

**Recommendation:**  
Disable the temporary HTTP service after testing and verify that TCP/8000 is no longer exposed.

**Limitation:**  
The assessment confirmed service exposure and HTTP response behavior but did not test for exploitation or establish vulnerability of the service.

---

### Target 2 — SSH Service Exposure on TCP/22

**Target:** Debian 13 Trixie — `192.168.1.141`

**Observation:**  
Nmap identified TCP/22 as an open SSH service and identified the service as OpenSSH 10.0p2 Debian 7+deb13u4.

**Evidence:**  
Nmap service/version enumeration against `192.168.1.141`.

**Security Relevance:**  
SSH represents a network-accessible administrative service and therefore contributes to the target's exposed service surface.

**Recommendation:**  
Confirm that SSH access is required for the intended laboratory configuration and restrict access appropriately where applicable.

**Limitation:**  
The assessment identified service exposure but did not perform credential attacks, exploitation, or vulnerability validation.

---

### OS Fingerprinting Observation

**Observation:**  
Nmap OS detection did not produce an exact operating system match for either authorized target.

**Security Relevance:**  
This demonstrates that automated OS fingerprinting can be inconclusive in virtualized laboratory environments.

**Limitation:**  
The actual operating systems were known from the laboratory configuration, so the Nmap results were treated as inconclusive rather than as definitive OS identification.

---

## 6. Target Comparison

| Attribute | Ubuntu Server | Debian 13 Trixie |
|---|---|---|
| IP Address | `192.168.1.120` | `192.168.1.141` |
| Host Status | Host is up | Host is up |
| Exposed Port | `8000/tcp` | `22/tcp` |
| Service | HTTP | SSH |
| Detected Version | SimpleHTTPServer 0.6 / Python 3.12.3 | OpenSSH 10.0p2 Debian 7+deb13u4 |
| OS Detection | Inconclusive | Inconclusive |
| Observation | Temporary HTTP service intentionally exposed for testing | SSH service available on the Debian target |

---

## 7. Recommendations

1. Disable temporary laboratory services after testing is complete.
2. Verify that TCP/8000 is no longer exposed after the HTTP testing activity.
3. Review whether SSH access on TCP/22 is required for the intended target configuration.
4. Restrict network-facing services to those required for the system's intended purpose.
5. Validate reconnaissance results using additional evidence where appropriate.
6. Maintain clear authorization boundaries when performing network scanning.

---

## 8. Limitations

The assessment was limited to the authorized laboratory targets created for this project.

The following activities were not performed:

- Exploitation of identified services
- Credential attacks
- Password cracking
- Unauthorized access attempts
- Scanning of external systems
- Scanning of unrelated systems within the shared environment
- Full vulnerability assessment of the target operating systems
- Production network testing

OS fingerprinting was also inconclusive for both targets.

An exposed service was not automatically treated as a vulnerability. Findings were limited to observations supported by the collected evidence.

---

## 9. Evidence

Evidence supporting this assessment is organized according to the project workflow.

```text
evidence/
├── 01-proxmox-target-vm/
├── 02-security-vm/
├── 03-connectivity/
├── 04-network-boundary/
├── 05-host-discovery/
├── 06-service-enumeration/
├── 07-os-identification/
├── 08-service-validation/
├── 09-second-target/
├── 10-target2-host-discovery/
├── 11-target2-service-enumeration/
└── 12-target2-os-identification/
```

The project contains 12 documented evidence items covering laboratory configuration, connectivity, reconnaissance, service enumeration, OS detection, service validation, and the second target assessment.

---

## 10. Conclusion

This laboratory demonstrated a structured and authorized approach to network reconnaissance within a controlled virtualized cybersecurity environment.

Nmap was used to identify reachable hosts, enumerate network services and versions, and perform OS fingerprinting. cURL was used to validate the HTTP service identified on the Ubuntu Server target.

The comparison between the Ubuntu Server and Debian 13 targets demonstrated that different systems can present different network-facing services.

The project also highlighted the importance of validating automated scan results, documenting limitations, and distinguishing observable service exposure from confirmed vulnerabilities.

These practices support accurate, evidence-based cybersecurity assessment and demonstrate practical skills relevant to network security and SOC/Blue Team activities.
