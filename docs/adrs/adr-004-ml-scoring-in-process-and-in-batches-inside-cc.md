# ADR-004: ML scoring in-process and in batches inside C&C

Context: FR-CC-001 requires analyzing all outbound traffic metadata - up to ~17,000 flows/s at XLarge. One model invocation per flow over a network hop cannot sustain this. AS-003 states the model is deployable Python code, not an external service.

Decision: The model runs inside the C&C process. C&C consumes the outbound topic in micro-batches of a few thousand flows and scores each batch in one pass.

Consequences / trade-offs: Throughput scales with Kafka partitions and C&C instances; no model-serving infrastructure is required. The cost we accept is that model updates require redeploying C&C, and C&C instances need the model's memory and CPU footprint.

What would falsify this decision: A need to update models independently of C&C releases, or to share one model across many services, would justify a separate model-serving service and its operational cost.
