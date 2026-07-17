# ADR-007: Capture-tier availability by fast restart, not feed duplication

Context: The capture tier sits before the event log; packets missed during an outage are unrecoverable as replay cannot restore what was never produced. The only alternatives are duplicating the entire mirror feed or restarting failed capture instances quickly.

Decision: Capture instances run under the container platform with health checks and automatic restart; at Medium/XLarge, traffic is split across multiple instances so one failure blinds only a fraction of traffic for seconds.

Consequences / trade-offs: A blind window of seconds per failure, well inside the 5-minute data-loss allowance of NFR-003, comes at near-zero extra cost. We do not pay for zero loss because no requirement demands it.

What would falsify this decision: A customer contract requiring zero packet loss during failures would force feed duplication for that deployment.
