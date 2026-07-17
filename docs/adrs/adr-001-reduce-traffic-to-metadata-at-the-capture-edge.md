# ADR-001: Reduce traffic to metadata at the capture edge

Context: At the XLarge tier the mirrored traffic is up to 50 Gbps. Publishing raw packets into the platform would mean hundreds of terabytes per day through every downstream component, while the functional requirements (FR-NF-002, FR-CC-001) only need flow metadata; only File Analysis needs payloads, and only for inbound POP3/FTP.

Decision: The Capture & Flow Export tier converts packets to compact flow records before anything enters the event log. Raw packets are never transported or stored. Payload handling is limited to reassembling inbound POP3/FTP sessions and extracting transferred files and complete e-mail messages for File Analysis.

Consequences / trade-offs: Roughly three orders of magnitude less data enters the platform, shrinking every downstream component. The cost we accept is that packet payloads are gone forever, so retroactive inspection of past traffic content is not possible.

What would falsify this decision: A requirement for full packet capture or retroactive payload inspection would invalidate this decision.
