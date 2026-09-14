# Configuration

Store only sanitized configuration.

Recommended layout as the project grows:

- `templates/` - human-maintained configuration sources;
- `vanilla/`, `tbc/`, `wotlk/` - era-specific fragments or policies;
- `effective/` - sanitized configuration captured from a concrete release.

Never commit real passwords, tokens, private connection strings, or an unsanitized `.env`.

A research result should reference the effective configuration for its server release, not only an intended template.
