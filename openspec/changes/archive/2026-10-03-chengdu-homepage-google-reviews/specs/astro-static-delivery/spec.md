## MODIFIED Requirements

### Requirement: Limit client runtime to interactive surfaces
The site SHALL deliver static presentation and article bodies without page-wide hydration. Client scripts or hydrated components SHALL be limited to the navigation, live business hours, galleries, dish dialogs, floating actions, video adaptation, telemetry, and an isolated Google reviews enhancement that actually need browser behavior. The reviews enhancement SHALL preserve a static heading and Google Maps link, load its third-party provider only according to the `google-review-display` capability, and require neither a persistent application server nor review-data requests during builds. Gatsby runtime MUST NOT be delivered.

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
