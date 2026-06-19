# Style Corpus Boundaries

Use this reference to decide what code should influence the Joseph Claus style profile.

## Include

- `joebot`
  - Discord bot, command handlers, API wrappers, tests, deployment-facing Docker assets.
- `spl-web`
  - React/MUI frontend, Redux Toolkit state, Express server APIs, webpack, tests.
- `spl-deployment`
  - Docker Compose, Nginx templates, deployment docs, GHCR/Watchtower conventions.
- `elgato/spl-soundboard`
  - Stream Deck plugin, newer TypeScript/ESM style, Rollup, Elgato SDK patterns.

## Exclude

- `joebot-old`
- Any repository not explicitly listed above.
- Generated dependencies, build output, vendored libraries, and third-party assets.
- Old or abandoned patterns when the active repo shows a newer local convention.

## How To Use The Corpus

When a task asks to match Joseph's coding style:

1. Inspect the active repo first.
2. If the active repo is one of the included corpus repos, use nearby files as the primary source of truth.
3. If the active repo is not in the corpus, use `coding-style.md` as a preference layer while still preserving that repo's existing conventions.
4. Prefer newer `elgato/spl-soundboard` patterns for new standalone TypeScript/ESM work.
5. Prefer `joebot` or `spl-web` patterns when modifying those legacy app surfaces.
