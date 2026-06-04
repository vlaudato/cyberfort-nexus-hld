# CyberFort Nexus — High-Level Design

A comprehensive enterprise cyber-defence detection system, designed as a capstone architecture project.

CyberFort Nexus is an on-premises detection platform installed at enterprise network gateways. It collects sensor data across inbound and outbound traffic, correlates threats through an automated cyber investigator, and provides SOC analysts with investigation, alerting, and forensic drill-down capabilities.

## Document Structure

| # | Document | Status | Description |
|---|----------|--------|-------------|
| 1 | [General](docs/01-general.md) | **In Progress** | Introduction, glossary, references |
| 2 | [Requirements](docs/02-requirements/) | **In Progress** | Functional and non-functional requirements, User Workflow |
| 3 | [High-Level Design](docs/03-high-level-design/) | Planned | Architecture, components, flows, data |
| 4 | [Time Estimation](docs/04-time-estimation.md) | Planned | Security architecture and threat model |
| 5 | [Limitations & Reservations](docs/05-limitations-reservations.md) | Planned | Capacity planning, sizing tiers, benchmarks |
| 6 | [Risks](docs/06-risks.md) | Planned | Known risks and mitigations |
| 7 | [Open Issues](docs/07-open-issues.md) | Planned | Open Issues |

## Architecture Decision Records

Significant design decisions are recorded as ADRs in [`docs/adrs/`](docs/adrs/).

## Diagrams

All diagrams live in [`diagrams/`](diagrams/) and are referenced from the documents.

- [Preliminary Solution Diagram](diagrams/preliminary-solution.png) — MS1 submission

## Milestones

- [x] **MS1** — Preliminary solution diagram
- [x] **MS2** — Requirements (Week 9)
- [ ] **MS3** — HLD + Data + Security + Performance diagrams (Week 13)
- [ ] **MS4** — Final submission