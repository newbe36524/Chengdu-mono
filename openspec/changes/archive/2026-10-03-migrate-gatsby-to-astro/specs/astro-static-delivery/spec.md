## Purpose

Define Chengdu's reproducible static-site development and delivery contract, including framework-runtime reduction, build artifact compatibility, and safe browser-only telemetry.

## ADDED Requirements

### Requirement: Provide reproducible static development and builds
The repository SHALL support `npm ci`, `npm run dev`, `npm start`, `npm run build`, `npm run serve`, `npm test`, and `npm run typecheck` on a supported Node.js 22 version. Builds SHALL produce the complete static site in `dist/` without invoking Gatsby or requiring a persistent application server.

#### Scenario: Build from a clean dependency installation
- **WHEN** a developer installs the lockfile with `npm ci` and runs `npm run build`
- **THEN** the build succeeds using the replacement toolchain and emits HTML, CSS, and assets under `dist/` without Gatsby-generated page data

#### Scenario: Preview the generated site
- **WHEN** a developer runs `npm run serve` after building
- **THEN** home, both menu URLs, listing pages, article deep links, redirects, and media can be accessed locally from the static artifact

### Requirement: Limit client runtime to interactive surfaces
The site SHALL deliver static presentation and article bodies without page-wide hydration. Client scripts or hydrated components SHALL be limited to the navigation, live business hours, galleries, dish dialogs, floating actions, video adaptation, and telemetry that actually need browser behavior. Gatsby runtime MUST NOT be delivered.

#### Scenario: Inspect generated content pages
- **WHEN** the generated home, menu, and article HTML and their first-party script dependencies are inspected
- **THEN** the main page/content trees are already rendered, only interactive boundaries start client code, and no Gatsby runtime or whole-page hydration entry exists

#### Scenario: Compare initial first-party JavaScript
- **WHEN** the migration and Gatsby baseline are measured on the same home, menu, and article URLs with the same viewport and cold-cache conditions
- **THEN** the migrated site's initially transferred first-party JavaScript bytes are lower for each representative route, with third-party analytics and fonts reported separately

### Requirement: Keep artifact consumers aligned
The configured CI build and static-host artifact upload SHALL consume `dist/` rather than the old generated `public/` directory. The sitemap-consuming IndexNow utility SHALL read generated sitemap URL entries from `dist/` without treating child-sitemap locations as page URLs.

#### Scenario: Inspect CI build configuration
- **WHEN** CI configuration is evaluated for a site change
- **THEN** the test workflow includes replacement framework configuration paths and the build workflow's size reporting and upload source both point to the generated static artifact

#### Scenario: Preview sitemap submission without network writes
- **WHEN** `node scripts/indexnow.js --dry-run` is run after a build
- **THEN** it reads the generated child sitemap files and reports page URLs without submitting requests or including sitemap XML URLs as pages

### Requirement: Preserve telemetry without blocking navigation
Production browser pages SHALL retain existing Clarity/Google tracking identifiers, button event names, and ordering conversion identifiers. Analytics SHALL initialize only when explicitly enabled for a production build; Google tracking SHALL continue respecting DNT and its existing excluded paths. Server-side builds, development, and non-production previews MUST NOT initialize telemetry.

#### Scenario: Build or browse a non-production preview
- **WHEN** a static build runs or a visitor opens a development/preview site without the production analytics flag
- **THEN** browser tracking is not initialized and normal links remain functional

#### Scenario: Select a tracked production action
- **WHEN** a visitor selects an ordering, menu, or location action on an analytics-enabled production page
- **THEN** the matching existing button event and applicable ordering conversion are attempted without suppressing the link's ordinary navigation

#### Scenario: Google tracking is excluded
- **WHEN** DNT is enabled or the current path matches an existing Google tracking exclusion
- **THEN** Google pageview and conversion requests are not sent

### Requirement: Document the replacement authoring contract
Repository documentation SHALL describe supported runtime/install commands, local development/preview, `dist/` output, existing Markdown and YAML authoring locations, preserved slug conventions, source static assets, and replacement analytics configuration.

#### Scenario: Follow local setup and article authoring instructions
- **WHEN** a contributor follows the updated README and article guide
- **THEN** the contributor can build and preview the site and add an article at its intended slug without relying on Gatsby commands or GraphQL setup
