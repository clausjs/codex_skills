---
name: github-tasks
description: Handle Git and GitHub workflow tasks for Joseph Claus repositories, including status review, branching, staging, commits, pushes, pull requests, issues, comments, and GitHub API or CLI changes. Use when Codex is asked to make git changes, create concise commits, split work into smaller commits, push branches, open or update PRs, use GitHub credentials, or perform repository-history tasks.
---

# GitHub Tasks

## Overview

Use this skill for source-control and GitHub operations. Pair it with `match-jclaus-style` when the same request also involves code changes.

## Workflow

1. Inspect the repository state before changing history: run `git status --short`, confirm the current branch, and review relevant diffs.
2. Protect user work: never revert, overwrite, amend, rebase, reset, or force-push changes unless the user explicitly asks for that exact operation.
3. Keep the work compartmentalized: stage only the files that belong to the requested change, and prefer multiple small commits when independent changes can be explained separately.
4. Use concise but descriptive commit messages that say what changed, such as `Add GitHub workflow skill` or `Document token-based GitHub access`.
5. Before committing, review `git diff --cached` or at least `git diff --cached --stat` so the commit contains only the intended paths.
6. After committing, report the commit subject and any follow-up GitHub state, such as pushed branch or PR URL.

## GitHub Authentication

Use `GITHUB_TOKEN` from the environment as the primary GitHub credential. Do not print token values.

- When repository instructions provide an environment loader, run GitHub commands through it. In this repository, use `scripts/with-codex-env`.
- Check token presence without revealing values, for example: `scripts/with-codex-env sh -lc 'test -n "${GITHUB_TOKEN:-${GH_TOKEN:-}}"'`.
- For `gh`, provide `GH_TOKEN` from `GITHUB_TOKEN` inside the loaded command when needed: `scripts/with-codex-env sh -lc 'GH_TOKEN="${GH_TOKEN:-$GITHUB_TOKEN}" gh pr status'`.
- For GitHub API calls, pass the token via an authorization header inside the loaded command. Avoid echoing headers, shell traces, or verbose logs that expose credentials.
- For authenticated GitHub git operations such as pushing an HTTPS remote, prefer the environment token through the loaded command or `gh` authentication flow instead of writing credentials into the repo.
- If a token is missing or lacks scope, stop and report the missing capability rather than inventing credentials or weakening authentication.

## Commit Hygiene

- Prefer small commits that map to one logical change: implementation, tests, docs, or plugin metadata can be separate commits when that makes history clearer.
- Avoid giant catch-all commits when the work naturally splits into independently reviewable pieces.
- Use straightforward commit subjects in sentence case or imperative style, matching the local repo's history when clear.
- Do not stage unrelated modified files. If unrelated user changes are present, leave them alone and mention that they were intentionally not included.
- When the user asks for a branch or PR, use the `codex/` branch prefix unless they request another name.

## GitHub Tasks

- For PRs, inspect the branch diff and include a clear summary plus the most relevant verification commands.
- For issue comments, PR reviews, labels, releases, or repository settings, use the GitHub CLI or API with the environment token.
- Prefer non-interactive commands. If an operation needs approval, request it before running the command.
- After pushing or creating a PR, report the URL and any checks that were started or observed.
