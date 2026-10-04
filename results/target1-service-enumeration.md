# Target 1 — Service & Version Enumeration

## Target

- **Hostname:** ubuntuserver
- **IP Address:** 192.168.1.120
- **Assessment Host:** Kali Linux (192.168.1.139)

## Objective

Identify exposed network services and determine their software and
version information on the authorized Ubuntu Server laboratory target.

## Command

nmap -sV -p 8000 192.168.1.120

## Result

PORT     STATE SERVICE VERSION
8000/tcp open  http    SimpleHTTPServer 0.6 (Python 3.12.3)

## Observation

Nmap identified TCP port 8000 as an open HTTP service running
SimpleHTTPServer 0.6 on Python 3.12.3.

The HTTP service was intentionally enabled within the controlled
laboratory environment for service enumeration and validation.

## Security Relevance

An actively reachable network service contributes to the target's
network attack surface.

The presence of the service alone does not establish a vulnerability
or exploitability.

## Validation

The identified HTTP service was subsequently validated using cURL:

curl -I http://192.168.1.120:8000

The service returned:

HTTP/1.0 200 OK
Server: SimpleHTTP/0.6 Python/3.12.3

## Assessment Conclusion

The scan successfully identified an intentionally exposed HTTP service
on TCP/8000. The result was validated through an HTTP response check.

The finding was documented as service exposure rather than automatically
classified as a vulnerability.
