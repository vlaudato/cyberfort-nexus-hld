# ADR-006: File Analysis processes events immediately, not periodically

Context: NFR-007 gives 60 seconds from detection to analyst visibility; a periodic batch that sleeps even one minute consumes the entire budget by itself. Inbound file and e-mail volume is small (AS-010), so there is no batching economy to collect - unlike C&C, where batching is justified by flow volume.

Decision: File Analysis consumes each `file.received` event as it arrives and scans immediately. The coupling remains asynchronous through the topic, so a File Analysis failure can never stall the capture tier; the log buffers and File Analysis catches up on restart.

Consequences / trade-offs: Files and e-mails are scanned immediately, minimizing the time required to detect threatening content. Processing each object individually introduces some overhead, but the expected volume is low enough that this cost is not significant.

What would falsify this decision: File and e-mail volumes high enough that individual AV calls saturate the 3rd-party engine would justify micro-batching toward the AV API.
