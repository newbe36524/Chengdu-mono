## 1. Locale foundation and authoritative English

- [x] 1.1 Add the typed locale registry, default `en-US`, and enabled-language list in `src/lib/i18n.ts`; initially keep incomplete non-English languages disabled.
- [x] 1.2 Implement recognized-prefix parsing, locale-preserving internal paths, equivalent page identities, trailing-slash behavior, and target-anchor-aware query/fragment enhancement without changing external or asset URLs.
- [x] 1.3 Inventory visitor-facing static and runtime text and add the complete `en-US` catalog, exact string-valued catalog types, safe interpolation, and nonempty/key-coverage validation.
- [x] 1.4 Add explicit `locale: en-US` to the existing 250 article files without changing bodies, stable slugs, dates, optional banners, or Sesame Chicken disambiguation.
- [x] 1.5 Add Jest cases for supported/disabled/unsupported locales, prefix boundaries, default English, route families, page-number/slug preservation, query/hash behavior, and catalog validation.

## 2. Locale-aware content and menu models

- [x] 2.1 Extend `src/content.config.ts` to require a supported locale and verify source-directory agreement while retaining existing metadata/date validation.
- [x] 2.2 Update `validateArticles` and related types for per-locale slug uniqueness, reserved listing paths, English counterpart identity, matching dates/banners, and enabled-language inventory parity with source diagnostics.
- [x] 2.3 Validate nonempty full Markdown bodies and reject copied English bodies and obvious translation placeholders; keep semantic completeness as an explicit review obligation.
- [x] 2.4 Update `getPublishedArticles(locale)` and article route helpers to filter enabled locales before presentation and preserve date/slug ordering and 12-item pagination.
- [x] 2.5 Extend menu YAML/types with group/item `translations` mappings, localized descriptions and ordered feature names; preserve all existing English/Chinese fields and nontext facts.
- [x] 2.6 Implement locale-specific menu display models and required-field parity validation with locale, source, prefix, code, and field diagnostics; preserve optional field absence.
- [x] 2.7 Add combined Jest coverage for missing/orphan/duplicate translation pairs, directory/date/banner errors, same slugs across locales, pagination parity, menu coverage, and preserved English defaults.

## 3. Shared static pages and existing interactive boundaries

- [x] 3.1 Extract the homepage body to `HomePage.astro` and listing body to `BlogListing.astro`; keep English wrappers and existing motion/layout hooks working.
- [x] 3.2 Thread explicit locale and equivalent-page identity through `Layout.astro`, `BlogPost.astro`, shared renderers, and each React island without hydrating entire pages.
- [x] 3.3 Add enabled-locale `getStaticPaths()` wrappers for translated home, both menus, listing pages, article pages, and explicit recovery pages; keep existing English routes unchanged.
- [x] 3.4 Localize homepage, restaurant features, footer, location, weekly hours, floating actions, and all visible/accessible labels through catalog lookups while preserving destinations and contact values.
- [x] 3.5 Localize article/listing framing, warnings, disclosures, variant conclusions, empty states, dates, pagination, link labels, and same-language recovery/location links.
- [x] 3.6 Localize featured/gallery dish data and island control/dialog text, including script-updated play/pause/error labels; retain existing image references, placeholders, keyboard behavior, and motion settings.
- [x] 3.7 Localize menu names, introductions, descriptions, features, notices, dialog labels, and optional secondary Chinese labels; retain all category/dish identities and modal focus behavior.
- [x] 3.8 Make menu viewport switching retain locale, search, and category fragment with no loops and preserve existing menu-pane scroll/history behavior.
- [x] 3.9 Localize calendar dates, weekdays, time display, statuses, and duration messages with native `Intl` APIs while retaining visitor-local calculations and minute refresh; extend existing hour-boundary tests.
- [x] 3.10 Update existing source-based motion tests to follow extracted renderer locations without weakening their behavior assertions.

## 4. Discoverable language control and localized metadata

- [x] 4.1 Add native `details`/`summary` language links with native names, localized labels, textual current-language state, `lang`/`hreflang`, and visible focus in `LanguageSwitcher.astro`.
- [x] 4.2 Integrate the switcher outside the mobile overlay and adjust header initial/focus/open visibility and layout so it is available on desktop/mobile, including the homepage hero.
- [x] 4.3 Add minimal query/fragment link enhancement using current URL and equivalent target anchor metadata, plus Escape disclosure dismissal; preserve working static links without scripts.
- [x] 4.4 Update SEO/document language for exact locales, localized text, self-canonicals, reciprocal enabled-language alternates, English `x-default`, social locale values, and existing absolute image URLs.
- [x] 4.5 Configure localized blog-root redirects and sitemap grouping/filtering in `astro.config.mjs`; exclude disabled locales, redirect-only pages, and localized recovery pages.
- [x] 4.6 Retain the global English `404.html`, render explicit localized recovery pages with `noindex`, and ensure recovery language choices target equivalent existing recovery routes.
- [x] 4.7 Normalize recognized locale prefixes in analytics exclusions and extend existing privacy tests without changing opt-in flags, DNT behavior, tracking events, or normal link navigation.
- [x] 4.8 Add only required wrapping and language-safe system font fallbacks; preserve existing red/gold identity and inspect long labels rather than shrinking text to fit.

## 5. Mexican Spanish interface and menu

- [x] 5.1 Complete the `es-MX` catalog for every static/runtime message and metadata field; review Mexican Spanish terminology and localized accessible labels.
- [x] 5.2 Add and review `es-MX` translations for menu groups A, B, C, D, and E, including every supplied item description and feature name.
- [x] 5.3 Add and review `es-MX` translations for menu groups F, G, K, L, and P, including every supplied item description and feature name.
- [x] 5.4 Add and review `es-MX` translations for menu groups R, S, T, V, and X, including every supplied item description and feature name.
- [x] 5.5 Complete and review Mexican Spanish featured/gallery descriptions, image alternatives, article framing, notices, and recovery text.

## 6. Mexican Spanish full article translations

Article batches in sections 6, 8, and 10 refer to the current 250 English articles sorted by stable frontmatter slug ascending, with one-based indexes and the existing Sesame Chicken disambiguation. Each batch includes translated frontmatter and the **entire** Markdown body, section-by-section review of all factual details and cautions, and localized same-site links. No batch is complete with titles, openings, or summaries alone. Do not add unrelated English articles while processing these batch boundaries.

- [x] 6.1 Translate and review `es-MX` articles 001-010.
- [x] 6.2 Translate and review `es-MX` articles 011-020.
- [x] 6.3 Translate and review `es-MX` articles 021-030.
- [x] 6.4 Translate and review `es-MX` articles 031-040.
- [x] 6.5 Translate and review `es-MX` articles 041-050.
- [x] 6.6 Translate and review `es-MX` articles 051-060.
- [x] 6.7 Translate and review `es-MX` articles 061-070.
- [x] 6.8 Translate and review `es-MX` articles 071-080.
- [x] 6.9 Translate and review `es-MX` articles 081-090.
- [x] 6.10 Translate and review `es-MX` articles 091-100.
- [x] 6.11 Translate and review `es-MX` articles 101-110.
- [x] 6.12 Translate and review `es-MX` articles 111-120.
- [x] 6.13 Translate and review `es-MX` articles 121-130.
- [x] 6.14 Translate and review `es-MX` articles 131-140.
- [x] 6.15 Translate and review `es-MX` articles 141-150.
- [x] 6.16 Translate and review `es-MX` articles 151-160.
- [x] 6.17 Translate and review `es-MX` articles 161-170.
- [x] 6.18 Translate and review `es-MX` articles 171-180.
- [x] 6.19 Translate and review `es-MX` articles 181-190.
- [x] 6.20 Translate and review `es-MX` articles 191-200.
- [x] 6.21 Translate and review `es-MX` articles 201-210.
- [x] 6.22 Translate and review `es-MX` articles 211-220.
- [x] 6.23 Translate and review `es-MX` articles 221-230.
- [x] 6.24 Translate and review `es-MX` articles 231-240.
- [x] 6.25 Translate and review `es-MX` articles 241-250.
- [x] 6.26 Confirm all 250 Mexican Spanish counterparts, catalog/menu parity, and review completion, then enable `es-MX` and confirm equivalent route/listing output.

## 7. Simplified Chinese Mandarin interface and menu

- [x] 7.1 Complete and review the `zh-CN` catalog for every static/runtime message and metadata field using Simplified Chinese Mandarin.
- [x] 7.2 Add and review complete `zh-CN` text for menu groups A, B, C, D, and E; reuse reviewed Chinese names but translate missing introductions, descriptions, and feature names.
- [x] 7.3 Add and review complete `zh-CN` text for menu groups F, G, K, L, and P, including supplied descriptions and feature names.
- [x] 7.4 Add and review complete `zh-CN` text for menu groups R, S, T, V, and X, including supplied descriptions and feature names.
- [x] 7.5 Complete and review Mandarin featured/gallery descriptions, image alternatives, article framing, notices, recovery text, and CJK rendering.

## 8. Simplified Chinese Mandarin full article translations

- [x] 8.1 Translate and review `zh-CN` articles 001-010.
- [x] 8.2 Translate and review `zh-CN` articles 011-020.
- [x] 8.3 Translate and review `zh-CN` articles 021-030.
- [x] 8.4 Translate and review `zh-CN` articles 031-040.
- [x] 8.5 Translate and review `zh-CN` articles 041-050.
- [x] 8.6 Translate and review `zh-CN` articles 051-060.
- [x] 8.7 Translate and review `zh-CN` articles 061-070.
- [x] 8.8 Translate and review `zh-CN` articles 071-080.
- [x] 8.9 Translate and review `zh-CN` articles 081-090.
- [x] 8.10 Translate and review `zh-CN` articles 091-100.
- [x] 8.11 Translate and review `zh-CN` articles 101-110.
- [x] 8.12 Translate and review `zh-CN` articles 111-120.
- [x] 8.13 Translate and review `zh-CN` articles 121-130.
- [x] 8.14 Translate and review `zh-CN` articles 131-140.
- [x] 8.15 Translate and review `zh-CN` articles 141-150.
- [x] 8.16 Translate and review `zh-CN` articles 151-160.
- [x] 8.17 Translate and review `zh-CN` articles 161-170.
- [x] 8.18 Translate and review `zh-CN` articles 171-180.
- [x] 8.19 Translate and review `zh-CN` articles 181-190.
- [x] 8.20 Translate and review `zh-CN` articles 191-200.
- [x] 8.21 Translate and review `zh-CN` articles 201-210.
- [x] 8.22 Translate and review `zh-CN` articles 211-220.
- [x] 8.23 Translate and review `zh-CN` articles 221-230.
- [x] 8.24 Translate and review `zh-CN` articles 231-240.
- [x] 8.25 Translate and review `zh-CN` articles 241-250.
- [x] 8.26 Confirm all 250 Mandarin counterparts, catalog/menu parity, and review completion, then enable `zh-CN` and confirm equivalent route/listing output.

## 9. Vietnamese interface and menu

- [x] 9.1 Complete and review the `vi` catalog for every static/runtime message and metadata field using Vietnamese.
- [x] 9.2 Add and review `vi` translations for menu groups A, B, C, D, and E, including every supplied item description and feature name.
- [x] 9.3 Add and review `vi` translations for menu groups F, G, K, L, and P, including every supplied item description and feature name.
- [x] 9.4 Add and review `vi` translations for menu groups R, S, T, V, and X, including every supplied item description and feature name.
- [x] 9.5 Complete and review Vietnamese featured/gallery descriptions, image alternatives, article framing, notices, recovery text, and diacritic rendering.

## 10. Vietnamese full article translations

- [x] 10.1 Translate and review `vi` articles 001-010.
- [x] 10.2 Translate and review `vi` articles 011-020.
- [x] 10.3 Translate and review `vi` articles 021-030.
- [x] 10.4 Translate and review `vi` articles 031-040.
- [x] 10.5 Translate and review `vi` articles 041-050.
- [x] 10.6 Translate and review `vi` articles 051-060.
- [x] 10.7 Translate and review `vi` articles 061-070.
- [x] 10.8 Translate and review `vi` articles 071-080.
- [x] 10.9 Translate and review `vi` articles 081-090.
- [x] 10.10 Translate and review `vi` articles 091-100.
- [x] 10.11 Translate and review `vi` articles 101-110.
- [x] 10.12 Translate and review `vi` articles 111-120.
- [x] 10.13 Translate and review `vi` articles 121-130.
- [x] 10.14 Translate and review `vi` articles 131-140.
- [x] 10.15 Translate and review `vi` articles 141-150.
- [x] 10.16 Translate and review `vi` articles 151-160.
- [x] 10.17 Translate and review `vi` articles 161-170.
- [x] 10.18 Translate and review `vi` articles 171-180.
- [x] 10.19 Translate and review `vi` articles 181-190.
- [x] 10.20 Translate and review `vi` articles 191-200.
- [x] 10.21 Translate and review `vi` articles 201-210.
- [x] 10.22 Translate and review `vi` articles 211-220.
- [x] 10.23 Translate and review `vi` articles 221-230.
- [x] 10.24 Translate and review `vi` articles 231-240.
- [x] 10.25 Translate and review `vi` articles 241-250.
- [x] 10.26 Confirm all 250 Vietnamese counterparts, catalog/menu parity, and review completion, then enable `vi` and confirm equivalent route/listing output.

## 11. Generated-artifact coverage and final integration

- [x] 11.1 Extend `tools/check-static-artifacts.js` to preserve English baseline assertions while deriving multilingual route counts and avoiding immutable baseline edits.
- [x] 11.2 Check every enabled locale's home, both menus, 250 articles, 21 listings, full body output, dates/order, warnings/disclosures, accessible labels, and working internal references.
- [x] 11.3 Check self-canonicals, reciprocal alternate links, `x-default`, document/social languages, sitemap inventory/filtering, localized redirects, unchanged static resources, and absence of whole-page/Gatsby runtime.
- [x] 11.4 Run relevant Jest selectors together for locale/content/menu/analytics/hour/motion behavior, then run existing `npm run typecheck`, `npm run build`, and `node tools/check-static-artifacts.js`; correct any related failures.
- [x] 11.5 Run `node scripts/indexnow.js --dry-run` against generated localized sitemaps and confirm only page URLs are reported without network submission.
- [ ] 11.6 Inspect desktop and mobile flows in all four languages, including 320px, 200% zoom, keyboard focus, no-JavaScript switching, article headings, menu resize/query/hash retention, and live localized labels (pending: no browser or browser automation tooling is available for the required viewport/zoom inspection).
- [x] 11.7 Confirm existing dialog Escape/focus restoration, gallery/video reduced-motion behavior, menu placeholders, authoritative contact/schedule values, analytics privacy, and external ordering behavior remain intact.
- [x] 11.8 Confirm all four locales are enabled with 1,000 complete article versions for the current 250-article inventory, 145 menu items per locale, and no untranslated-body or disabled-language omissions.

## 12. Authoring and design documentation

- [x] 12.1 Update `README.md` and `docs/how-to-post.md` with locale identifiers/directories, translation-pair rules, full-body review checklist, Mexican Spanish conventions, and required paired updates after English edits.
- [x] 12.2 Document language activation/completeness diagnostics, URL-based preference, preserved English URLs, localized internal links, and the global static-host 404 limitation.
- [x] 12.3 Update `PRODUCT.md` for the confirmed language/audience scope and `DESIGN.md` plus `.impeccable/design.json` for the language control and intentional header changes, preserving unrelated tokens and product facts.
