# ADR-003: Persistence follows data shape: columnar + relational + object storage

Context: The system has three data populations with incompatible access patterns: netflow/detections/scan-reports (append-only at up to ~17,000 records/s sustained at XLarge, queried by time range and filter over 90 days, NFR-006); alerts/investigations/users (low volume, fetched and updated individually, with ownership and integrity rules, FR-INVP-003/008); extracted files and e-mail messages (opaque binaries, written once, fetched by key, subject to retention).

Decision: Three stores, each matching one shape. Columnar analytical database for append-only time-range data; relational database for mutable owned entities; S3-compatible object storage for binaries, with lifecycle rules implementing retention.

Consequences / trade-offs: Each store does only what it is good at. The cost we accept is three technologies to install, patch, back up, and monitor at every customer site. Rejected alternatives: one relational database for everything (write path collapses at XLarge ingest rates while serving 30-day scans); a search-engine store for netflows (indexes every field at write time and stores 2-3x the raw size).

What would falsify this decision: A requirement for free-text search across netflow fields would reopen the search-engine alternative; snapshot or scan-report growth beyond projections would reopen sizing.
