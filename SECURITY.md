# Security and sensitive data

This is a public repository. Treat every committed file as permanently public.

Never publish:

- passwords, API tokens, SSH keys, or private certificates;
- real `.env` files;
- private IP addresses or remote-access credentials when they are not required for reproduction;
- account databases or live character database dumps;
- personal email addresses or player-identifying data;
- Blizzard client files, MPQ archives, or copyrighted game assets.

Use sanitized examples for configuration. Use stable pseudonymous IDs such as `BOT-C01-0042` instead of internal account identifiers.

If a secret is committed, rotate the secret first. Removing it from the latest commit is not sufficient because Git history may preserve it.
