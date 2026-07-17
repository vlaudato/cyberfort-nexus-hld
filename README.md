# CyberFort Nexus — High-Level Design

A comprehensive enterprise cyber-defence detection system, designed as a capstone architecture project.

CyberFort Nexus is an on-premises detection platform installed at enterprise network gateways. It collects sensor data across inbound and outbound traffic, correlates threats through an automated cyber investigator, and provides SOC analysts with investigation, alerting, and forensic drill-down capabilities.

## Document Structure

| # | Document | Status | Description |
|---|----------|--------|-------------|
| 1 | [General](docs/01-general.md) | Complete | Introduction, glossary, references |
| 2 | [Requirements](docs/02-requirements/) | Complete | Functional and non-functional requirements, user workflows, sizing |
| 3 | [High-Level Design](docs/03-high-level-design/) | **In Progress** | Architecture, runtime processes, design principles, upgradability |
| 4 | [Time Estimation](docs/04-time-estimation.md) | Complete | Rough-order-of-magnitude implementation effort by workstream |
| 5 | [Risks](docs/05-risks.md) | Complete | Architecture risks and mitigations |

## Architecture Decision Records

Significant design decisions are recorded as ADRs in [`docs/adrs/`](docs/adrs/).

## Diagrams

All diagrams live in [`diagrams/`](diagrams/) and are referenced from the documents.

- [Preliminary Solution Diagram](diagrams/preliminary-solution.png) — MS1 submission
- [Component and Data Flow Diagram](diagrams/component-data-flow-diagram.png) — logical components and interactions
- [Logical Deployment View](diagrams/logical-deployment-view.png) — logical on-premises deployment groups and external interactions

## Milestones

- [x] **MS1** — Preliminary solution diagram
- [x] **MS2** — Requirements (Week 9)
- [x] **MS3** — HLD + Data + Security + Performance diagrams (Week 13)
- [x] **MS4** — Final submission
