# Target 1 — OS Detection

## Target

- **Hostname:** ubuntuserver
- **IP Address:** 192.168.1.120
- **Assessment Host:** Kali Linux (192.168.1.139)

## Objective

Identify the operating system characteristics of the authorized Ubuntu
Server laboratory target using Nmap OS detection.

## Command

sudo nmap -O 192.168.1.120

## Result

Nmap returned a Linux/router-oriented fingerprint rather than identifying
the installed Ubuntu Server distribution.

The target was not conclusively identified as Ubuntu by Nmap.

## Observation

The actual target operating system was Ubuntu Server, but Nmap's automated
OS fingerprinting did not provide an exact Ubuntu identification.

This demonstrates that OS detection results should be interpreted as
fingerprint-based observations rather than definitive identification.

## Security Relevance

OS fingerprinting can provide useful information for understanding the
likely operating system characteristics of a target.

However, inaccurate or inconclusive fingerprinting can occur, particularly
in virtualized laboratory environments.

## Assessment Conclusion

Nmap OS detection produced a Linux/router-oriented fingerprint but did not
accurately identify the Ubuntu Server distribution.

The result was therefore treated as inconclusive rather than as a
definitive operating system identification.
