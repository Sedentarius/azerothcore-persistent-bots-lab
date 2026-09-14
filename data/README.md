# Data

Published research data should be sanitized, documented, and linked to a stable dataset ID.

Recommended lifecycle:

`raw -> intermediate -> processed -> published`

Published raw data are immutable. If a published dataset contains an error, create a corrected dataset ID and mark the old dataset as deprecated.

Each published dataset should eventually include:

- `README.md`;
- machine-readable metadata;
- schema or data dictionary;
- checksums;
- source experiment/session IDs;
- units and null semantics;
- transformation provenance when it is not raw data.

Large datasets should not be forced into Git if GitHub Releases or a research archive is more suitable.
