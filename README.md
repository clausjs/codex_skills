# Codex Skills

This repo holds personal Codex plugins, skills, and references for Claus Products development workflows.

The current plugin is `claus-products`, which includes the `match-jclaus-style` skill. That skill captures coding-style guidance from selected Joseph Claus projects and helps Codex keep future code changes consistent with those patterns.

## Repo Layout

```text
plugins/
  claus-products/
    .codex-plugin/
      plugin.json
    skills/
      match-jclaus-style/
        SKILL.md
        agents/openai.yaml
        references/
          coding-style.md
          repo-corpus.md
```

Use this repo as the editable source of truth. For local testing, copy `plugins/claus-products` into whichever plugin directory your Codex marketplace entry points to.

## Creation Notes

This plugin was created with Codex's plugin and skill authoring workflow:

- Scaffold a plugin manifest at `plugins/claus-products/.codex-plugin/plugin.json`.
- Add the `match-jclaus-style` skill under `plugins/claus-products/skills/`.
- Store the detailed coding-style profile in skill reference files instead of putting everything in `SKILL.md`.
- Register the plugin in a personal or repo marketplace during local testing.

The style profile was seeded from representative Claus Products repositories by name, not from machine-specific paths. The initial corpus was:

- `joebot`
- `spl-web`
- `spl-deployment`
- `elgato/spl-soundboard`

Old, abandoned, generated, vendored, or third-party code should stay out of the corpus.

## GitHub Access

Use a GitHub token from Codex's environment rather than committing credentials to this repo. `GITHUB_TOKEN` is this repo's convention for GitHub access; it is not a Codex-reserved variable.

Recommended variable:

```bash
GITHUB_TOKEN=<your-token>
```

Optional alias for GitHub CLI compatibility:

```bash
GH_TOKEN=$GITHUB_TOKEN
```

For style analysis and repository inspection, the token should have read access to the repositories Codex is allowed to inspect. For a fine-grained GitHub token, start with repository metadata and contents read access for the selected repos. Add broader scopes only when a task actually needs them.

Never commit tokens, `.env` files with secrets, shell history exports, or generated credential files.

This repo includes an ignored local env file for Codex-related secrets:

```text
.env.codex.local
```

Put private values there while working locally:

```bash
GITHUB_TOKEN=<your-token>
GH_TOKEN=$GITHUB_TOKEN
```

For commands that need those variables, run through the loader script:

```bash
scripts/with-codex-env <command>
```

For example:

```bash
scripts/with-codex-env node scripts/github-task.js
```

The loader makes the variables available to that command and any child processes. Codex does not automatically source arbitrary env files for every shell command, so repository instructions tell Codex to use this loader whenever repo-local secrets are needed.

## Setup

1. Put the GitHub token in the environment available to Codex.

   In a shell-run workflow:

   ```bash
   export GITHUB_TOKEN=<your-token>
   export GH_TOKEN=$GITHUB_TOKEN
   ```

   In the Codex app, prefer the app or project environment/secrets settings when available, so the token is injected at runtime without being written into this repo.

2. Install `gh` only if you want CLI-based GitHub workflows.

   ```bash
   brew install gh
   gh auth status
   ```

   If `gh auth status` is not authenticated, run:

   ```bash
   gh auth login
   ```

3. Keep the plugin manifest valid after edits.

   Use Codex's `plugin-creator` workflow to validate the plugin and bump the plugin version/cachebuster after changes. If you are not using that helper, manually update the `version` field in `plugins/claus-products/.codex-plugin/plugin.json` before reinstalling so Codex notices the new local build.

4. Copy the editable plugin to the plugin directory referenced by your marketplace.

   ```bash
   mkdir -p <plugin-install-root>/plugins
   cp -R plugins/claus-products <plugin-install-root>/plugins/
   ```

5. Confirm your marketplace entry points at the installed plugin.

   ```json
   {
     "name": "claus-products",
     "source": {
       "source": "local",
       "path": "./plugins/claus-products"
     },
     "policy": {
       "installation": "AVAILABLE",
       "authentication": "ON_INSTALL"
     },
     "category": "Productivity"
   }
   ```

   The `source.path` value should be relative to the marketplace root.

6. Restart Codex after local plugin or marketplace changes so the app reloads the plugin metadata.

## Updating The Style Skill

Use these files for normal style-profile edits:

- `plugins/claus-products/skills/match-jclaus-style/SKILL.md`
- `plugins/claus-products/skills/match-jclaus-style/references/coding-style.md`
- `plugins/claus-products/skills/match-jclaus-style/references/repo-corpus.md`

Keep the style corpus narrow. Include only repos Joseph identifies as representative, and explicitly exclude old or third-party code so the skill does not learn the wrong habits.
