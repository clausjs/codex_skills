# Repository Instructions

Before running commands that need repository-local secrets or environment variables, load `.env.codex.local` through `scripts/with-codex-env`.

Example:

```bash
scripts/with-codex-env env | rg '^(GITHUB_TOKEN|GH_TOKEN)='
```

Do not print secret values in normal output. Check for presence only unless the user explicitly asks for a value.

`.env.codex.local` is intentionally ignored by git and should never be committed.
