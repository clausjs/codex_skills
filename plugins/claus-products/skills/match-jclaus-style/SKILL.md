---
name: match-jclaus-style
description: Follow Joseph Claus coding style, implementation preferences, and development-routine instincts when Codex is editing code, reviewing code, adding tests, changing deployment files, or making architecture choices in Joseph's projects. Use when the user asks to match their style, work in joebot, spl-web, spl-deployment, elgato/spl-soundboard, or otherwise make coding changes that should feel consistent with Joseph's existing TypeScript, React, Express, Docker, and deployment conventions.
---

# Match Jclaus Style

## Overview

Use this skill as a preference layer for coding tasks, not as a replacement for reading the current repository. The active repo and nearby code always win when they conflict with this profile.

## Workflow

1. Identify the active repo and task surface.
2. Read nearby files, package scripts, tests, and config before editing.
3. Read `references/repo-corpus.md` to confirm whether the repo should influence Joseph's style profile.
4. Read `references/coding-style.md` before making implementation choices.
5. Make the smallest coherent change that fits the local owner module.
6. Verify with the repo's existing scripts when practical, and report any command that could not be run.

## Style Priorities

- Preserve the local repo's module system, formatting, quotes, and testing style.
- Prefer direct, feature-local implementation over broad abstraction.
- Use descriptive domain names and practical helper functions.
- Keep unrelated refactors and formatting churn out of the diff.
- Add tests when behavior changes or a regression would be easy to miss.

## Reference Files

- `references/repo-corpus.md`: included and excluded repositories for style inference.
- `references/coding-style.md`: concrete implementation preferences extracted from the selected repos.
