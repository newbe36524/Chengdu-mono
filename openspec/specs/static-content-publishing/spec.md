## Purpose

Keep Chengdu's existing Markdown articles, published URLs, paginated discovery, metadata, and static assets accessible to readers and crawlers independently of client rendering.

## Requirements

### Requirement: Preserve article URLs and complete content
The site SHALL publish every currently eligible Markdown article at `/blog` followed by its existing frontmatter `slug`, without deriving public URLs from source filenames. Article titles, opening text where currently shown, dates, Markdown structure, optional banners, and internal links MUST be preserved.

The two Sesame Chicken source files currently share `/how-to-make-sesame-chicken`. Preserve that established URL for `dish-E3-芝麻鸡.md` (the article currently emitted by Gatsby) and publish `dish-C6-芝麻鸡.md` at the unique `/how-to-make-sesame-chicken-c6` slug so both source articles remain available without a route collision.

#### Scenario: Open an existing article URL directly
- **WHEN** a reader requests an existing `/blog/how-to-make-fuqi-feipian` URL or any other eligible frontmatter-based article path
- **THEN** a static article page contains its original title and body without requiring a client-side route transition

#### Scenario: Render optional banners and Unicode asset names
- **WHEN** an article has a banner reference containing a Unicode filename, or has no banner field
- **THEN** the matching existing image renders correctly in the first case and the article renders normally without a banner in the second

#### Scenario: Preserve an unavailable optional banner
- **WHEN** an article references an image that is absent from the authored image tree
- **THEN** the build reports the source article and missing asset, and the article remains available without a banner, matching the incumbent Gatsby output

### Requirement: Preserve content-specific article presentation
The site SHALL preserve recipe, story, tool, cuisine, culture, Tulsa, and generic article variants selected by their existing slug prefixes. Existing AI disclosures, recipe warnings, closing sections, pickup/delivery actions, and location actions SHALL appear for the same variants as before.

#### Scenario: Read a recipe article
- **WHEN** a reader opens an article whose slug starts with `/how-to-make`
- **THEN** its opening, optional dish banner, tutorial warning, rendered body, dish-specific restaurant conclusion, and AI disclosures are present

#### Scenario: Read non-recipe article variants
- **WHEN** a reader opens a story, tool, cuisine, culture, Tulsa, or unmatched-prefix article
- **THEN** the appropriate established introductory and concluding content is retained without incorrectly inserting the recipe tutorial

### Requirement: Preserve blog ordering and pagination
The site SHALL order eligible articles by date descending, render 12 articles per page except the final page, and preserve `/blog/{page}` listing URLs, article title links, dish labels where supplied, opening summaries, formatted dates, and previous/next/numbered pagination. `/blog` SHALL forward to `/blog/1`.

#### Scenario: Browse the current article inventory
- **WHEN** the current 250 eligible articles are built
- **THEN** 21 listing pages are available, the first 20 contain 12 entries each, and the final page contains 10 entries

#### Scenario: Follow pagination boundaries
- **WHEN** a visitor browses the first or final listing page
- **THEN** no previous link is shown on the first page, no next link is shown on the final page, and all numbered links target existing pages

#### Scenario: Dates are tied
- **WHEN** multiple articles have the same date
- **THEN** every article appears exactly once across listing pages and repeated builds produce a stable order within each date group

#### Scenario: No eligible articles exist
- **WHEN** the content source contains no eligible articles
- **THEN** `/blog/1` shows an explicit empty state, `/blog` still forwards there, and no invalid pagination links are generated

### Requirement: Surface invalid publishing inputs
The build SHALL report invalid required article metadata, malformed dates, duplicate article URLs, and collisions between article URLs and numbered listing routes with actionable source-path diagnostics. Invalid content MUST NOT silently disappear from an otherwise successful build.

#### Scenario: Conflicting or malformed article input
- **WHEN** an article slug duplicates another slug, resolves to `/blog/1`, or its required title/date/slug is invalid
- **THEN** the build fails and identifies the offending source and validation problem

### Requirement: Preserve page metadata and crawlable outputs
The site SHALL emit page-specific titles, descriptions, keywords where used, absolute canonical URLs, Open Graph/Twitter metadata, document language, available social images, sitemap files, robots policy, and manifest/icon references using `https://www.chengdufoodtulsa.com` as the production origin. These outputs MUST NOT require client JavaScript.

#### Scenario: Inspect an article and listing page
- **WHEN** a crawler reads the generated HTML for an article or blog listing
- **THEN** it receives the corresponding title, description, production canonical URL, and an absolute social image URL with an existing fallback when no banner is supplied

#### Scenario: Discover routes from the sitemap
- **WHEN** a crawler retrieves `/robots.txt` and `/sitemap-index.xml`
- **THEN** the policy permits crawling, the sitemap is reachable, and its child sitemap includes all published article and listing URLs but excludes not-found and redirect-only pages

### Requirement: Preserve static files and not-found behavior
The static artifact SHALL contain the existing IndexNow verification file, host configuration, site icons/manifest, image/video assets, and a branded not-found page with recovery links. Unknown routes MUST NOT be rewritten to a successful home page.

#### Scenario: Request a missing path
- **WHEN** a visitor requests an unknown route on the configured static host
- **THEN** the host responds with status 404 and the branded page offers working home, blog, order, and location links

#### Scenario: Retrieve static resources
- **WHEN** a browser or verifier requests a referenced image, video, icon, manifest, or IndexNow verification file
- **THEN** the file is served from the generated artifact at its intended URL without a client router fallback
