## MODIFIED Requirements

### Requirement: Preserve article URLs and complete content
The site SHALL publish every currently eligible English Markdown article at `/blog` followed by its existing frontmatter `slug`, without deriving public URLs from source filenames. Each enabled non-English language SHALL publish its complete translated counterpart at `/{locale}/blog` followed by the same slug. Titles, opening text where currently shown, dates, Markdown structure, optional banners, and internal links MUST retain equivalent content in the selected language; English URLs and authored English content MUST remain intact.

The two Sesame Chicken source files currently share `/how-to-make-sesame-chicken`. Preserve that established URL for `dish-E3-芝麻鸡.md` (the article currently emitted by Gatsby) and publish `dish-C6-芝麻鸡.md` at the unique `/how-to-make-sesame-chicken-c6` slug so both source articles remain available without a route collision. Translations SHALL use these same disambiguated slugs.

#### Scenario: Open an existing article URL directly
- **WHEN** a reader requests an existing `/blog/how-to-make-fuqi-feipian` URL or any other eligible frontmatter-based English article path
- **THEN** a static article page contains its original title and body without requiring a client-side route transition

#### Scenario: Render optional banners and Unicode asset names
- **WHEN** an article has a banner reference containing a Unicode filename, or has no banner field
- **THEN** the matching existing image renders correctly in the first case and the article renders normally without a banner in the second, in every enabled language

#### Scenario: Preserve an unavailable optional banner
- **WHEN** an article references an image that is absent from the authored image tree
- **THEN** the build reports the source article and missing asset, and the article remains available without a banner, matching the incumbent Gatsby output

#### Scenario: Read a translated existing article
- **WHEN** a visitor opens `/zh-CN/blog/how-to-make-fuqi-feipian/`
- **THEN** a complete Simplified Chinese article renders in delivered HTML with the same stable article identity and existing assets

### Requirement: Preserve blog ordering and pagination
For each enabled language, the site SHALL publish the same eligible article inventory, order articles by date descending with stable slug ordering for ties, and render 12 articles per page except the final page. English SHALL preserve `/blog/{page}` URLs; translated listings SHALL use `/{locale}/blog/{page}`. Article title links, dish labels where supplied, opening summaries, dates, and previous/next/numbered pagination SHALL be localized and remain in the selected language. `/blog` SHALL forward to `/blog/1`, and `/{locale}/blog` SHALL forward to `/{locale}/blog/1`.

#### Scenario: Browse the current article inventory
- **WHEN** the current 250 eligible articles and their complete translations are built
- **THEN** each enabled language has 21 listing pages, the first 20 contain 12 entries each, and the final page contains 10 entries

#### Scenario: Follow pagination boundaries
- **WHEN** a visitor browses the first or final listing page in any enabled language
- **THEN** no previous link is shown on the first page, no next link is shown on the final page, and all numbered links target existing same-language pages

#### Scenario: Dates are tied
- **WHEN** multiple articles have the same date
- **THEN** every article appears exactly once across listing pages and repeated builds produce a stable order within each date group, identical by article identity across languages

#### Scenario: No eligible articles exist
- **WHEN** the English content source and its translation inventory contain no eligible articles
- **THEN** each enabled language's first listing shows a localized explicit empty state, its blog root still forwards there, and no invalid pagination links are generated

### Requirement: Preserve page metadata and crawlable outputs
The site SHALL emit localized page-specific titles, descriptions, keywords where used, absolute self-canonical URLs, Open Graph/Twitter metadata, document language matching the exact locale identifier, available social images, sitemap files, robots policy, and manifest/icon references using `https://www.chengdufoodtulsa.com` as the production origin. Every indexed localized page SHALL emit reciprocal alternate links for its equivalent pages in all enabled languages and an `x-default` alternate pointing to its English counterpart. These outputs MUST NOT require client JavaScript.

#### Scenario: Inspect an article and listing page
- **WHEN** a crawler reads the generated HTML for an article or blog listing in any enabled language
- **THEN** it receives the corresponding localized title and description, self-canonical production URL, exact document language, reciprocal alternate links, and an absolute social image URL with an existing fallback when no banner is supplied

#### Scenario: Discover routes from the sitemap
- **WHEN** a crawler retrieves `/robots.txt` and `/sitemap-index.xml`
- **THEN** the policy permits crawling, the sitemap is reachable, and its child sitemaps include all published home, menu, article, and listing URLs in enabled languages but exclude not-found and redirect-only pages

#### Scenario: A translation is not enabled
- **WHEN** a language is disabled during incremental implementation
- **THEN** metadata and sitemap outputs do not advertise its routes as available translations
