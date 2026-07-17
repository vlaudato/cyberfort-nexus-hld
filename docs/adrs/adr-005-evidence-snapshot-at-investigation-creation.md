# ADR-005: Evidence snapshot at investigation creation, stored in the Relational DB

Context: Netflow data is deleted after 3 months (FR-NF-004), but investigations live longer and must remain reviewable (FR-INVP-005); ACI-created content is immutable (FR-INVP-006). References into the analytical store would silently rot when retention deletes the underlying records; pinning referenced records against deletion would make retention non-deterministic and the sizing table untrue.

Decision: When an investigation is created (by the ACI or manually via the Portal), the correlated evidence - alerts and supporting netflow records - is copied into an immutable snapshot stored with the investigation in the Relational DB.

Consequences / trade-offs: Retention stays exact; investigations keep their evidence indefinitely. Storage cost is negligible: hundreds-to-thousands of ~100-byte records per investigation, well under 1 GB/year at projected volumes. Storing snapshots in the Relational DB (rather than Bucket Storage) keeps the read path to a single store; we accept revisiting this if snapshots grow large.

What would falsify this decision: If analysts routinely need to re-run full-window queries on old investigations rather than review frozen evidence, longer netflow retention would be the right lever instead.
