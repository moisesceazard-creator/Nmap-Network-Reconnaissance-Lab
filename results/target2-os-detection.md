# Target 2 — OS Detection

## Target

- **Hostname:** Debian 13 Trixie
- **IP Address:** 192.168.1.141
- **Assessment Host:** Kali Linux (192.168.1.139)

## Objective

Identify the operating system characteristics of the authorized Debian 13
laboratory target using Nmap OS detection.

## Command

sudo nmap -O 192.168.1.141

## Result

Nmap did not identify an exact operating system match for the target.

A TCP/IP fingerprint was generated for further analysis.

## Observation

Although the target was known to be running Debian 13 Trixie, Nmap's
automated OS fingerprinting did not provide an exact operating system
identification.

## Security Relevance

OS fingerprinting can provide useful information about the likely
characteristics of a target and support reconnaissance activities.

However, an inconclusive fingerprint should not be treated as definitive
operating system identification.

## Assessment Conclusion

Nmap generated a TCP/IP fingerprint for the authorized Debian 13 target
but did not identify an exact operating system match.

The result was therefore treated as inconclusive and demonstrates the
limitations of automated OS fingerprinting in the virtualized laboratory
environment.
