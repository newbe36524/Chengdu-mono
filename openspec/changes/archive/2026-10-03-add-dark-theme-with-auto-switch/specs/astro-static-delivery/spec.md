## MODIFIED Requirements

### Requirement: Limit client runtime to interactive surfaces
The site SHALL deliver static presentation and article bodies without page-wide hydration. Client scripts or hydrated components SHALL be limited to the navigation, theme initialization and switching, live business hours, galleries, dish dialogs, floating actions, video adaptation, telemetry, and an isolated Google reviews enhancement that actually need browser behavior. Theme initialization SHALL be a bounded pre-paint enhancement shared across content routes; manual switching MUST NOT require whole-page hydration or a persistent application server. Convertible presentation and interactions SHALL render through native Astro HTML with bounded browser enhancements and MUST NOT deliver React or React DOM runtime code. Any retained React boundary MUST have a documented technical blocker, its affected routes and interaction scope, and an explicit removal strategy; static presentation MUST NOT be included in that exception's hydration boundary. With no justified exception, generated pages and their first-party script dependency graph MUST contain no React hydration entry or runtime. The reviews enhancement SHALL preserve a static heading and Google Maps link, load its third-party provider only according to the `google-review-display` capability, and require neither a persistent application server nor review-data requests during builds. Gatsby runtime MUST NOT be delivered.

#### Scenario: Inspect generated content pages
- **WHEN** the generated home, menu, and article HTML and their first-party script dependencies are inspected
- **THEN** the main page/content trees are already rendered, only interactive boundaries start client code, and no Gatsby runtime or whole-page hydration entry exists

#### Scenario: Compare initial first-party JavaScript
- **WHEN** the migration and Gatsby baseline are measured on the same home, menu, and article URLs with the same viewport and cold-cache conditions
- **THEN** the migrated site's initially transferred first-party JavaScript bytes are lower for each representative route, with third-party analytics and fonts reported separately

#### Scenario: Generate static artifacts without review-provider access
- **WHEN** the site is built with reviews disabled or with complete enabled configuration but without network access to Google Places
- **THEN** static generation does not request reviews, the homepage fallback is emitted, and no server endpoint or serialized Google review response is required

#### Scenario: Open unrelated routes
- **WHEN** a visitor opens a menu, blog, privacy, or terms route without the reviews section
- **THEN** no review-specific client enhancement initializes and no review-provider SDK or details request starts

#### Scenario: Browse migrated restaurant interactions
- **WHEN** a visitor uses featured-card expansion, gallery navigation and playback, fullscreen dish information, or current business hours on an enabled-locale homepage
- **THEN** these surfaces function without a React runtime while satisfying the existing `restaurant-site-experience` requirements for content, keyboard access, responsive behavior, focus restoration, no-JavaScript essentials, and local-clock updates

#### Scenario: Compare against the current React homepage
- **WHEN** the pre-migration React/Astro homepage and migrated homepage are measured with identical content, enabled locales, flags, browser, viewport, cold-cache conditions, and interaction sequence
- **THEN** cumulative first-party JavaScript transferred through calendar initialization and gallery activation is lower in the migrated version, initial first-party JavaScript does not increase, and representative menu and article routes do not gain homepage-only enhancement code
- **AND** measurements identify initial versus enhancement-triggered transfers, separate third-party traffic, and report generated JavaScript size and build duration without asserting an unmeasured build-speed improvement

#### Scenario: Complete migration without exceptions
- **WHEN** all assessed React fragments have native equivalents and the static site is built
- **THEN** no React hydration entries or React runtime dependencies are reachable from any generated page, and contributor documentation identifies no retained React exception

#### Scenario: A fragment cannot be migrated directly
- **WHEN** implementation identifies a concrete technical blocker preventing equivalent native behavior
- **THEN** the migration record identifies the fragment, blocker, affected routes, smallest required interactive boundary, and removal strategy before React is retained, and unaffected converted surfaces remain framework-free

#### Scenario: Initialize and switch themes on static routes
- **WHEN** a visitor opens home, menu, or article content and changes the theme
- **THEN** a pre-paint bootstrap and a bounded control enhancement provide the behavior without page-wide hydration, React/Gatsby runtime, or homepage-only enhancement code on unrelated routes
