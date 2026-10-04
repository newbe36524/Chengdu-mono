## Purpose

Provide complete, consistent translations of Chengdu's visitor-facing content while preserving American English as the authoritative version and preventing partial language versions from being published.

## ADDED Requirements

### Requirement: Complete localized visitor-facing text
Every enabled language SHALL provide home-page copy, navigation, ordering labels, menu notices, dish and category text, gallery descriptions, image alternatives, dialog text, business-hour labels, article framing, footer, empty states, error controls, recovery-page content, and metadata. Accessible and script-updated labels SHALL use the page language. Product names, addresses, URLs, telephone numbers, dish codes, and intended cultural names SHALL retain their factual identity.

#### Scenario: Inspect a localized page and its interactions
- **WHEN** a visitor browses an enabled non-English language and opens menu details, gallery controls, navigation, or the live calendar
- **THEN** the displayed and accessible text is in the selected language, including labels changed after interaction or hydration

#### Scenario: Missing localized menu description
- **WHEN** a dish has an English description but lacks that description in an enabled language
- **THEN** the build fails and identifies the language, dish code, field, and source rather than publishing an English fallback

### Requirement: Full article translations
For every published English article, each enabled language SHALL provide a counterpart with the same stable slug and publication date, translated title and opening, translated dish label where present, and a complete translated Markdown body. Translation SHALL preserve the meaning and complete information in paragraphs, headings, lists, tables, quotations, recipes, cautions, image alternatives, and link labels. Summaries, copied English bodies, placeholders, and omitted sections MUST NOT count as completed translations. Shared introductions, warnings, conclusions, and AI disclosures SHALL also be translated.

#### Scenario: Read a fully translated recipe
- **WHEN** a reader opens any enabled-language recipe article
- **THEN** every ingredient, preparation step, tip, caution, and conclusion is available in that language with the original factual quantities and instructions retained

#### Scenario: An article only has a translated title
- **WHEN** a proposed translation has localized metadata but an absent, empty, copied English, or summary-only body
- **THEN** publication readiness fails through automated structural checks or documented content review and the language is not considered complete

#### Scenario: Translate non-recipe content
- **WHEN** a story, tool, cuisine, culture, Tulsa, or generic article is translated
- **THEN** all authored sections and the matching variant's introductory and concluding content remain available in the selected language

### Requirement: American English authority and regional language quality
`en-US` SHALL be the complete source version, including authoritative government and business information where present. `es-MX` translations SHALL use Mexican Spanish, not a Spain-oriented version; `zh-CN` SHALL use Simplified Chinese Mandarin; `vi` SHALL use Vietnamese. Translations MUST NOT fabricate claims or change contact details, hours, ordering destinations, factual amounts, or safety cautions. Changes to English information SHALL be accompanied by corresponding updates and review in every enabled language before publication.

#### Scenario: Review Mexican Spanish content
- **WHEN** the Spanish version is reviewed for readiness
- **THEN** visitor-facing copy uses Mexican Spanish vocabulary and conventions and identifies its language as `es-MX`

#### Scenario: Change authoritative information
- **WHEN** an English article or restaurant business detail changes
- **THEN** all enabled-language counterparts are updated and reviewed for equivalent meaning before the changed content is considered publication-ready

### Requirement: Actionable completeness diagnostics
Publishing validation SHALL reject unsupported locale metadata, absent English counterparts, duplicate locale/slug pairs, missing enabled-language counterparts, invalid required fields, and incomplete menu or message coverage. Diagnostics SHALL identify the source and affected locale and content identity. Identical slugs in different languages SHALL be permitted; duplicate slugs within one language SHALL remain errors.

#### Scenario: A counterpart is missing
- **WHEN** an English article has no Vietnamese counterpart while `vi` is enabled
- **THEN** the build fails with the missing locale and article slug rather than reducing the Vietnamese listing inventory

#### Scenario: Duplicate versus shared slugs
- **WHEN** two articles use the same slug within `es-MX`, or matching articles use it once each in `en-US` and `es-MX`
- **THEN** the first case fails with source diagnostics and the second case is accepted as a translation pair
