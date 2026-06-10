# 2. Requirements

This section captures both functional and non-functional requirements for CyberFort Nexus, derived from the project specification and refined through architectural analysis.

## Functional Requirements

| Section | Scope |
|---------|-------|
| [2.1 Logical — System Functionality](2.1-logical-requirements.md) | What each subsystem detects, processes, and produces |
| [2.2 User Workflow](2.2-user-workflow.md) | SOC analyst interactions and investigation flows |

## Non-Functional Requirements

| Section | Scope |
|---------|-------|
| [2.3 Availability & Recovery](2.3-availability.md) | Uptime targets, failure modes, recovery objectives |
| [2.4 Performance & Capacity](2.4-performance.md) | Throughput, latency, sizing tiers |
| [2.5 Scalability](2.5-scalability.md) | Growth model, scaling axes, elasticity |
| [2.6 Security](2.6-security.md) | Security requirements at all layers |
| [2.7 Monitoring & Debugging](2.7-monitoring.md) | Observability, health, diagnostics |
| [2.8 Deployment](2.8-deployment.md) | Deployment model, packaging, platform constraints |
| [2.9 Backward Compatibility](2.9-compatibility.md) | Upgrade paths, data migration |

## Assumptions

The following assumptions are given by the project specification or derived during architectural analysis. They are **preconditions** that the system design depends on but that CyberFort Nexus does not control.

| ID | Assumption | Source |
|----|------------|--------|
| **AS-001** | The organisation's gateway switch can mirror (copy) all IP traffic — inbound, outbound, and duplex — to a dedicated monitoring port without affecting the original traffic flow | Project spec |
| **AS-002** | CyberFort Nexus connects to the monitoring port via a passive probe (network interface) that receives all mirrored traffic in read-only mode. CyberFort never injects or modifies live traffic. | Project spec |
| **AS-003** | A pre-trained ML model for C&C detection is available as Python code. Training, retraining, and model selection are out of scope | Project spec |
| **AS-004** | The 3rd-party File Analysis engine is available as a deployable component with a REST API. Licensing and procurement are out of scope | Project spec |
| **AS-005** | Inbound email traffic uses POP3 protocol. Inbound file transfer traffic uses FTP protocol. | Project spec |
| **AS-006** | The C&C detection threshold of 0.70 is assumed pending empirical validation with production traffic. The actual value would be determined through testing with the ML model. Configurability was deliberately excluded to simplify capacity planning and eliminate the risk of misconfiguration. This would be revisited if the product required multi-tenant deployment or customer-specific tuning. | Project spec |
| **AS-007** | Recovery Time Objective (RTO) and Recovery Point Objective (RPO) are derived from industry average attack frequency (~1636 threats every week minutes per organisation) | [SentinelOne - Key Cyber Security Statistics for 2026](https://www.sentinelone.com/cybersecurity-101/cybersecurity/cyber-security-statistics/) |
| **AS-008** | Average network activity is 100 IP flows per minute per endpoint | Project spec |
| **AS-009** | A single netflow record is approximately 100 bytes including storage overhead | Engineering estimate |
| **AS-010** | File Analysis retained storage is negligible relative to Netflow storage. Based on industry average email volume (~40 emails/endpoint/day), malware infection rate (~0.1%) and average malicious payload (~2 MB), infected file retention at XLarge is estimated at ~72 GB over 3 months, that accounts to ~1% of the Netflow capacity. FTP file transfer volume is considered negligible in modern enterprise networks | Engineering estimate, infection rate from [Verizon DBIR](https://www.verizon.com/business/resources/reports/dbir/) |
| **AS-011** | A single FA scan log entry is approximately 1 KB, estimated from the expected AV scan response JSON structure including storage overhead. | Engineering estimate |
| **AS-012** | Only suspected C&C activity (above threshold) is logged. Logging all analysis results would duplicate netflow metadata at significantly higher storage cost (~52 TB/year at XLarge) with no additional forensic value. | Architectural decision |
| **AS-013** | C&C detection rate is estimated at ~0.0002% of outbound flows, derived from SOC analyst alert handling capacity (~174 alerts/analyst/day) and CyberFort's estimated share of total alert volume (~15%). See [C&C Log Storage derivation in §2.4](2.4-performance-capacity.md#cc-log-storage-1-year-retention) for the full calculation. | Engineering estimate; alert capacity from [Vectra AI 2026, Prophet Security 2025](https://www.prophetsecurity.ai/blog/soc-capacity-modeling-how-many-alerts-can-your-team-really-handle) |


## Conventions

- Functional requirements use prefixed IDs based on subsystem:
  - `FR-SYS-xxx` — System-level / cross-cutting
  - `FR-FA-xxx` — File Analysis
  - `FR-CC-xxx` — Command & Control Detection
  - `FR-NF-xxx` — Network Forensics
  - `FR-ACI-xxx` — Automatic Cyber Investigator
  - `FR-INVP-xxx` — Investigation Portal
- Non-functional requirements use `NFR-xxx`.
- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.
- Each NFR includes a **measurable acceptance criterion**.