# 1. General

## 1.1 Introduction

CyberFort Nexus is a next-generation on-premises enterprise cyber-defense solution. It is deployed at the gateway of an enterprise network, where it inspects inbound, outbound and duplex traffic through threat-detection sensors. Detected events are logged and analyzed by an Automatic Cyber Investigator, which surfaces attack campaigns and alerts to SOC analysts through an Investigation Portal.

The system is **detection-only**, meaning it doesn’t perform mitigation or active response to cyber-attacks.

## 1.2 Glossary

| Term | Definition |
|------|-----------|
| **Netflow** | Metadata about network connections (source, destination, ports, timestamps, byte counts) without full packet payload |
| **Security Operations Center (SOC)** | A team of cyber-security analysts who monitor and respond to security events |
| **Command and Control Engine (C&C)** | ML engine that detects suspected outbound traffic |
| **File Analysis Engine** | Third-party anti-virus software that scans all inbound files and emails |
| **Forensic Engine** | Engine that indexes all inbound and outbound traffic as a Netflow |
| **Automatic Cyber Investigator (ACI)** | The core part of the system. It gets the data from all the engines and alerts on cyber incidents |
| **Investigation Portal** | Tool exposed to SOC analysts, where they can perform investigations and drill down on events and network forensics |

## 1.3 References

| Ref       | Document                                                                                                 |
| -----------| ----------------------------------------------------------------------------------------------------------|
| [PROJECT] | CyberFort Nexus — Course Project Specification                                                           |
| [RFC2119] | Key words for use in RFCs to Indicate Requirement Levels — https://datatracker.ietf.org/doc/html/rfc2119 |

---

[2. Requirements →](02-requirements/README.md)