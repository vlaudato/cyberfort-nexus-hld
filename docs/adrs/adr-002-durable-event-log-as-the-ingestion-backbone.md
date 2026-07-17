# ADR-002: Durable event log as the ingestion backbone (not point-to-point queues)

Context: The GW Switch continuously sends mirrored traffic, and the Capture & Flow Export tier cannot pause or replay that feed since it is a live feed. Flow records must therefore be handed off quickly to durable storage so temporary downstream failures do not cause permanent data loss. The same streams must be consumed independently by multiple components.

Decision: A single durable, replayable event log carries all inter-component streams (`inbound`, `outbound`, `file.received`, `alert.raised`). Consumers track their own position and replay after failure. No other queues are introduced anywhere in the system.

Consequences / trade-offs: The event log buffers temporary traffic bursts, allows multiple components to consume the same events independently, and retains events so consumers can resume processing after a failure. These capabilities support the five-minute Recovery Point Objective defined by NFR-003. The accepted cost is the hardware capacity and operational effort required to run and maintain a durable clustered event log, including in the Small deployment tier.

What would falsify this decision: If the Small tier's hardware budget cannot accommodate a minimal log cluster, the Small deployment profile would need a simplified variant.
