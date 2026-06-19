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
- `clausjs/clausjs.github.io`
  - Personal site, static frontend structure, CSS, small-site conventions.
- `clausjs/Discord-Bot-Status-Watcher`
  - TypeScript Discord bot patterns, status-monitoring workflows, service checks.
- `clausjs/discord_bot_starter`
  - JavaScript Discord bot starter conventions and practical command scaffolding.
- `clausjs/express-reactRouter-scaffold`
  - TypeScript Express plus React Router scaffold patterns for new app foundations.
- `clausjs/webhook-torrent-reporter`
  - TypeScript webhook integration patterns and small service structure.

## Exclude

- `joebot-old`
- `spl-web-dev`
- `clausjs/LuckPerms`
- `clausjs/discord-embed-visualizer`
- `clausjs/grubhub-scraper`
- `clausjs/homepage`
- `clausjs/mini-qr`
- `clausjs/obs-studio`
- `clausjs/srs`
- `clausjs/teamworkdreamwork-hubot`
- `clausjs/torrent-parser`
- `clausjs/data_structures_practice`
- `nit3owl/teacher-timer`
- Any repository not explicitly listed above.
- Generated dependencies, build output, vendored libraries, and third-party assets.
- Old or abandoned patterns when the active repo shows a newer local convention.

## How To Use The Corpus

When a task asks to match Joseph's coding style:

1. Inspect the active repo first.
2. If the active repo is one of the included corpus repos, use nearby files as the primary source of truth.
3. If the active repo is not in the corpus, use `coding-style.md` as a preference layer while still preserving that repo's existing conventions.
4. Prefer newer `elgato/spl-soundboard` patterns for new standalone TypeScript/ESM work.
5. Prefer `express-reactRouter-scaffold` patterns when starting a new Express/React app from scratch.
6. Prefer `joebot`, `Discord-Bot-Status-Watcher`, or `discord_bot_starter` patterns when modifying Discord bot surfaces.
7. Prefer `joebot` or `spl-web` patterns when modifying those legacy app surfaces.
