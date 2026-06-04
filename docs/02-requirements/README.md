# 2. Requirements

This section captures both functional and non-functional requirements for CyberFort Nexus, derived from the project specification and refined through architectural analysis.


## Functional Requirements

| Section                                              | Scope                                                |
| ------------------------------------------------------| ------------------------------------------------------|
| [2.1 Logical — System Functionality](2.1-logical-requirements.md) | What each subsystem detects, processes, and produces |
| [2.2 User Workflow](2.2-user-workflow.md)            | SOC analyst interactions and investigation flows     |

## Non-Functional Requirements

| Section                                            | Scope                                              |
| ----------------------------------------------------| ----------------------------------------------------|
| [2.3 Availability & Recovery](2.3-availability.md) | Uptime targets, failure modes, recovery objectives |
| [2.4 Performance & Capacity](2.4-performance.md)   | Throughput, latency, sizing tiers                  |
| [2.5 Scalability](2.5-scalability.md)              | Growth model, scaling axes, elasticity             |
| [2.6 Security](2.6-security.md)                    | Security requirements at all layers                |
| [2.7 Monitoring & Debugging](2.7-monitoring.md)    | Observability, health, diagnostics                 |
| [2.8 Deployment](2.8-deployment.md)                | Deployment model, packaging, platform constraints  |
| [2.9 Backward Compatibility](2.9-compatibility.md) | Upgrade paths, data migration                      |

## Assumptions

The following assumptions are given by the project specification or derived during architectural analysis. They are **preconditions** that the system design depends on but that CyberFort Nexus does not control.

| ID         | Assumption                                                                                                                                                                                                  | Source       |
| ------------| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| --------------|
| **AS-001** | The organisation's gateway switch can mirror (copy) all IP traffic — inbound, outbound, and duplex — to a dedicated monitoring port without affecting the original traffic flow.                            | Project spec |
| **AS-002** | CyberFort Nexus connects to the monitoring port via a passive probe (network interface) that receives all mirrored traffic in read-only mode. CyberFort never injects or modifies live traffic.             | Project spec |
| **AS-003** | A pre-trained ML model for C&C detection is available as Python code. Training, retraining, and model selection are out of scope.                                                                           | Project spec |
| **AS-004** | The 3rd-party File Analysis engine is available as a deployable component with a REST API. Licensing and procurement are out of scope.                                                                      | Project spec |
| **AS-005** | Inbound email traffic uses POP3 protocol. Inbound file transfer traffic uses FTP protocol.                                                                                                                  | Project spec |
| **AS-006** | The default C&C detection threshold of 0.70 is assumed pending empirical validation with production traffic. The actual value would be determined through testing with the ML model, which is out of scope. | Project spec |

## Conventions

- Functional requirements use prefixed IDs based on subsystem:
  - `FR-SYS-xxx` — System-level / cross-cutting
  - `FR-FA-xxx` — File Analysis
  - `FR-CC-xxx` — Command & Control Detection
  - `FR-NF-xxx` — Network Forensics
  - `FR-ACI-xxx` — Automatic Cyber Investigator
  - `FR-INVP-xxx` — Investigation Portal
- Non-functional requirements use `NFR-xxx`.
- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
      NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and
      "OPTIONAL" in this document are to be interpreted as described in
      RFC 2119.
- Each NFR includes a **measurable acceptance criterion**.