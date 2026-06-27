# Joseph Claus Coding Style Profile

This profile was derived from representative Claus Products source samples in these repositories:

- `joebot`
- `spl-web`
- `spl-deployment`
- `elgato/spl-soundboard`
- `clausjs/clausjs.github.io`
- `clausjs/Discord-Bot-Status-Watcher`
- `clausjs/discord_bot_starter`
- `clausjs/express-reactRouter-scaffold`
- `clausjs/webhook-torrent-reporter`

Do not infer style from `joebot-old`, unrelated local clones, third-party repositories, or projects the user did not identify as representative.

## Core Instincts

- Prefer direct, feature-local code over frameworky indirection.
- Add helpers when they remove repeated mechanics, not just to make abstractions symmetrical.
- Keep behavior close to the feature that owns it: commands in command files, API route logic in route files, React event handlers near the component state they affect.
- Favor explicit names for domain concepts: `SoundboardClip`, `fetchSoundboardClips`, `generatePIPayloadFromClips`, `DEFAULT_SOCKET_URL`.
- Accept pragmatic local state and imperative browser/API work when it is the simplest readable path.
- Preserve existing project style before applying this profile. The active repo wins when it conflicts with this document.
- Comment larger implementation blocks when their purpose is not immediately obvious. Keep comments focused on what the block achieves or why the approach exists, not on line-by-line narration.

## TypeScript And JavaScript

- Match the module system already in the package. Use CommonJS in older Express server files that already use `require`; use ESM imports in TypeScript and newer Elgato plugin code.
- Use TypeScript types where the file already has TypeScript, especially for props, payloads, state shapes, and return values.
- Keep type definitions readable and local when they are only used in one feature.
- Prefer `const` for values and helper functions. Use `let` for intentionally reassigned values.
- Use early returns for guard clauses.
- Prefer OOP (object-oriented programming) in JavaScript/TypeScript for domain behavior, stateful services, and shared boundaries: use classes or clear object models when they make ownership and lifecycle easier to follow.
- Do not chase perfect type purity at the cost of a large unrelated refactor. If the existing code uses a little `any` or looser typing around third-party APIs, keep changes scoped and improve only what the task touches.

## Formatting Signals

- Follow the surrounding file first.
- Existing code commonly uses 4-space indentation in TypeScript/React and semicolons.
- Quotes vary by area: older app code often uses single quotes; newer Elgato code often uses double quotes. Match the file.
- Keep object and array literals easy to scan, with multiline formatting for larger option sets and payloads.
- Avoid broad reformatting. Do not run formatters across unrelated files unless the repo already expects that for the task.

## React And Frontend

- Prefer functional components with hooks.
- Put each React component in its own file unless it is a tiny render helper that would be harder to read on its own.
- Organize UI code into folders that match the feature or UI surface, with colocated component, test, style, and helper files when the existing project supports that structure.
- When creating or reshaping React project structure, use Joseph's other React projects as the preference layer: feature-oriented UI folders, readable component boundaries, and filenames that make the screen easy to parse for a human.
- Keep component-specific event handlers in the component when they are tightly coupled to local state.
- Use Redux Toolkit patterns where the existing state layer uses them.
- Use MUI components/icons in `spl-web` rather than inventing custom primitives for standard UI controls.
- Keep UI behavior practical: state names should describe what the screen needs, such as `isSearching`, `dialogOpen`, `editingClip`, `nowPlaying`.
- Avoid landing-page or marketing-style rewrites when working on internal app screens. Focus on the usable workflow.

## Backend And APIs

- In Express route files, follow the existing pattern of small route handlers with `try/catch`, `req.isTesting` branches where present, and straightforward HTTP status responses.
- Keep external API wrappers thin and domain-named.
- Preserve existing environment-variable names and deployment assumptions.
- Handle service failures with clear logs or returned errors, but avoid introducing a new global error framework unless asked.

## Tests

- Add or update tests when behavior changes, especially command handlers, API routes, reducers, and parsing helpers.
- For React projects, add functional tests with React Testing Library for components, hooks, and user-visible flows touched by the change.
- Add Playwright e2e tests when the repo has, or can reasonably support, a runnable browser app and the change affects navigation, integration behavior, auth/session flow, or a critical user workflow.
- Do not stop at e2e coverage for React changes. Prefer the pairing of focused React Testing Library tests plus one or more Playwright paths when the workflow can be exercised end to end.
- For backend and server components, add unit tests at minimum. Broaden to integration or Supertest-style route coverage when request/response behavior, persistence, or external service boundaries are part of the change.
- Use the repo's current test style. In `joebot`, Mocha tests use helper assertions and descriptive `describe` blocks. In `spl-web`, server tests use Mocha/Supertest-style patterns.
- Prefer focused tests around the changed behavior over broad snapshot-style assertions.
- If Playwright or React Testing Library is missing from a React project, prefer adding the missing tool only when it is practical for the current task and consistent with the package manager and scripts already in use.

## Deployment And Ops

- Keep deployment docs practical and command-oriented.
- Preserve branch/tag conventions: `main` for production, `dev` for staging, GHCR image tags by branch where applicable.
- When changing Docker, Nginx, or environment docs, include verification commands and the expected operational effect.

## Review Checklist

Before finishing code in this style:

- Does the change live in the feature/module that already owns the behavior?
- Did you avoid unrelated rewrites and broad formatting churn?
- Are names domain-specific and obvious without being clever?
- Did you match the current file's module system, quote style, and typing strictness?
- For React changes, did you add or update React Testing Library coverage and Playwright e2e coverage when practical?
- For backend/server changes, did you add unit tests at minimum?
- Are tests or verification commands aligned with the repo's existing scripts?
- Are larger, non-obvious implementation blocks commented at the right level of detail?
- Would the resulting code feel practical to maintain next month?
