# Target 2 — Service & Version Enumeration

## Target

- **Hostname:** Debian 13 Trixie
- **IP Address:** 192.168.1.141
- **Assessment Host:** Kali Linux (192.168.1.139)

## Objective

Identify exposed network services and determine their software and
version information on the authorized Debian 13 laboratory target.

## Command

nmap -sV 192.168.1.141

## Result

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 10.0p2 Debian 7+deb13u4 (protocol 2.0)

Service Info: OS: Linux

## Observation

Nmap identified TCP port 22 as an open SSH service running
OpenSSH 10.0p2 on Debian.

The SSH service was observed as an actively reachable network service
on the authorized laboratory target.

## Security Relevance

An exposed SSH service contributes to the target's network attack surface.

The presence of an open SSH service alone does not establish a
vulnerability or compromise.

## Assessment Conclusion

The scan successfully identified an SSH service on TCP/22 and provided
its software and version information.

The result was documented as service exposure and inventory information
rather than automatically classified as a vulnerability.
