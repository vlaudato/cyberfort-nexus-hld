# ADR-006: File Analysis processes events immediately, not periodically

Context: NFR-007 gives 60 seconds from detection to analyst visibility; a periodic batch that sleeps even one minute consumes the entire budget by itself. Extracted-file volume (inbound mail attachments and FTP files) is small (AS-010), so there is no batching economy to collect - unlike C&C, where batching is justified by flow volume.

Decision: File Analysis consumes each `file.received` event as it arrives and scans immediately. The coupling remains asynchronous through the topic, so a File Analysis failure can never stall the capture tier; the log buffers and File Analysis catches up on restart.

Consequences / trade-offs: Files are scanned immediately, minimizing the time required to detect malicious content. Processing each file individually introduces some overhead, but the expected file volume is low enough that this cost is not significant.

What would falsify this decision: File volumes high enough that per-file AV calls saturate the 3rd-party engine would justify micro-batching toward the AV API.
