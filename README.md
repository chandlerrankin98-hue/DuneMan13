# Arrakis Companion

A mobile-first companion for *Dune: Awakening* on PS5. This repository is the source home for the React, TypeScript and Vite app, including project planning, nested build checklists, catalog references, and local save/recovery tools.

## Current status

- **Production:** [arrakis-companion.pages.dev](https://arrakis-companion.pages.dev/) remains on the previously released version 1.3.0. Publishing source here does not change the live site.
- **Preview:** [projects-ui-preview.arrakis-companion.pages.dev](https://projects-ui-preview.arrakis-companion.pages.dev/) is the separate test site.
- **Projects:** each project keeps its own counts. Expand a target for its required parts, then a part for its direct ingredients. Recording owned/completed quantities does not spend crafting ingredients.
- **Catalog:** references are partial. Unknown recipes and quantities stay marked unknown or incomplete; references do not prove current PS5 behavior.
- **Saves:** browser saves, account saves, and cloud acknowledgement are distinct. Export a backup before deliberate restore or profile replacement.

See the [roadmap](docs/ROADMAP.md), [project brief](docs/PROJECT_OVERHAUL_BRIEF.md), [development guide](docs/DEVELOPMENT.md), [tests](docs/TESTING.md), [save and recovery design](docs/SYNC_FOUNDATION.md), and [deployment guide](docs/DEPLOYMENT.md).

## Run locally

Use Node.js 24 and npm:

```bash
npm ci
npm run dev
```

Open the loopback URL Vite prints, normally `http://127.0.0.1:5173`. Keep the terminal running, and stop it with `Control+C`. Open the app through Vite, not by opening `index.html` directly.

## Verify changes

```bash
npm test
npm run test:sources
npm run test:sync:sql
npm run format:check
npm run build
```

The build type-checks the app and writes static output to `dist/`. The SQL tests use an isolated fixture; they do not connect to production.

## Architecture

| Directory | Responsibility |
| --- | --- |
| `src/features/`, `src/components/` | Screens, navigation, and shared controls |
| `src/domain/` | Planning, quantities, allocations, and inventory rules |
| `src/data/` | Curated and generated public reference data |
| `src/storage/` | Validated state, local journals, backups, and recovery |
| `src/sync/` | Account-specific cache and revision-checked sync adapter |
| `supabase/`, `tests/sql/` | Reviewed SQL and isolated policy fixtures |
| `scripts/` | Catalog import and verification |
| `docs/`, `release/` | Decisions, roadmap, operations, and release records |

## Data, privacy, and licensing

Public catalog data and private player progress are separate. Never commit `.env.local`, provider credentials, private backups, or player exports. The ignore rules cover local configuration, dependencies, build output, backups, and browser test artifacts. `.env.example` contains blank public browser configuration fields; never put service-role keys, OAuth secrets, or database passwords in `VITE_` variables.

Some catalog records derive from the Dune: Awakening Community Wiki, whose source is attributed in [data provenance](docs/IMPORT_SOURCES.md) and licensed CC BY-NC-SA 4.0. Preserve that attribution and applicable share-alike terms. Game content remains the property of its respective rights holders. No blanket license is granted here for original application code; absent a license, all rights are reserved.

## Preview and deployment

For a local static preview, run `npm run build` and `npm run preview`. Review [deployment guidance](docs/DEPLOYMENT.md) before a hosted release. Cloudflare Pages uses Direct Upload. Upload only reviewed static output from `dist/`, never the project directory, environment files, private backups, screenshots, or player saves. Production publication requires explicit release approval.
