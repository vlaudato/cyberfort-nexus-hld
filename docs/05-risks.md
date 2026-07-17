# 5. Risks

| ID | Risk and potential impact | Mitigation |
|----|---------------------------|------------|
| R-001 | Capture overload or failure can cause unrecoverable gaps because mirrored traffic cannot be replayed. | Performance-test every sizing tier, monitor packet drops, restart failed instances automatically, and split the feed across instances at larger tiers (ADR-007). |
| R-002 | The machine-learning model or the assumed 0.70 threshold may produce excessive false positives or miss real C&C activity. | Validate the model with representative traffic, record the model version with each detection, and monitor detection rates before accepting the threshold (AS-006). |
| R-003 | Antivirus capacity, availability, or licensing limits may create a backlog and breach the 60-second alert-visibility target. | Test scan throughput, monitor API latency and `file.received` consumer lag, and provision sufficient antivirus capacity for the selected tier. |
| R-004 | Actual flow, file, or scan-report volumes may exceed the sizing assumptions and exhaust storage before retention expires. | Monitor storage growth, enforce lifecycle rules, alert on capacity thresholds, and expand storage according to NFR-011. |
| R-005 | A durable event-log cluster may consume a disproportionate share of the Small tier's resources. | Benchmark the minimum supported deployment profile; if it cannot satisfy the Small-tier workload, revisit ADR-002 while preserving the single software baseline required by NFR-010. |

---

← [4. Time Estimation](04-time-estimation.md)
