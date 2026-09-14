# Scripts

Planned script families:

- `realm/` - start/stop and session accounting;
- `manifest/` - server and release manifests;
- `cohort/` - controlled cohort creation;
- `export/` - sanitized research exports;
- `telemetry/` - derived metrics and health records;
- `backup/` - verification helpers for private backups.

Scripts that touch production data should default to safe, read-only behavior unless mutation is their explicit purpose.
