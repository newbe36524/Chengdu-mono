## 1. Capture the Existing Site Contract

- [x] 1.1 In `repos/chengdu/`, inventory all current page/article URLs, Markdown metadata, menu groups/items, ordering destinations, tracked static files, and existing sitemap/icon outputs; retain the baseline outside generated source directories.
- [x] 1.2 Capture incumbent desktop/mobile screenshots for home, both menus, blog lists, and representative article variants, plus navigation, gallery, and drawer states; use current CSS/assets as the appearance baseline.
- [x] 1.3 Record cold-cache initial first-party JavaScript bytes for representative home/menu/article routes under matching viewport conditions; record third parties separately and document any baseline blocker rather than claim unmeasured improvement.
- [x] 1.4 Run the existing business-hour tests and record the visitor-local time, 768px menu routing, gallery interaction, and tracking contracts described in the capability specs.

## 2. Establish the Astro Toolchain

- [x] 2.1 Add compatible stable Astro, React and sitemap integrations, Astro checking support, and a declared YAML parser; keep the supported Node.js 22 runtime and npm lockfile.
- [x] 2.2 Add `astro.config.mjs` with static output, production site origin, `dist/`, trailing-slash behavior, and `/blog` redirect; configure Astro/Vite types in `tsconfig.json` and environment declarations.
- [x] 2.3 Replace `dev`, `start`, `build`, and `serve` scripts with Astro commands; make `typecheck` cover `.astro` and non-Astro TypeScript, retain Jest, and ensure `clean` never deletes authored `public/`.
- [x] 2.4 Adapt PostCSS/Tailwind and CSS-module import wiring without redesigning styles; retain CommonJS compatibility for Jest and `scripts/indexnow.js`.

## 3. Migrate Content and Asset Loading

- [x] 3.1 Add `src/content.config.ts` over the existing Markdown tree with original public slugs, required metadata validation, valid date parsing, and optional dish/banner handling.
- [x] 3.2 Implement shared article route, variant, date-order/tie-breaker, and 12-item pagination helpers in `src/lib/content.ts`; reject duplicate/traversing slugs and numbered listing collisions with source-path diagnostics.
- [x] 3.3 Implement typed YAML loading in `src/lib/menus.ts`, preserving prefix sorting, item order, bilingual fields, descriptions, and features; surface malformed data and duplicate identifiers.
- [x] 3.4 Implement `src/lib/images.ts` with imported Unicode-safe local asset resolution, optimized image descriptors for React islands, and banner/social-image transformations; retain deliberate image-less menu placeholders.
- [x] 3.5 Move only authored `static/` files into source `public/`, preserve the verification file, add robots/manifest and reproducible icon replacements, and update `.gitignore` for `public/`, `dist/`, and `.astro/`.

## 4. Port the Shared Shell and Restaurant Home

- [x] 4.1 Create `src/layouts/Layout.astro` with the incumbent visibility props and port section wrappers, restaurant features, location/contact/map, and footer to static markup using existing copy/CSS.
- [x] 4.2 Port desktop/mobile navigation to normal links with focused toggle/scroll scripts; retain menu links and Visit Us behavior on pages lacking a local location section, with keyboard/focus/scroll-lock handling.
- [x] 4.3 Port pickup, delivery, menu, location, and floating actions to ordinary anchors; preserve external URLs/new-tab behavior and hero-dependent floating visibility without requiring tracking.
- [x] 4.4 Replace `src/pages/index.tsx` with `index.astro`, preserving section order, hero identity, address tooltip, 480p/720p background video behavior, fonts, and usable autoplay/reduced-motion fallback.
- [x] 4.5 Adapt `MainGallery.tsx`, `GridGallery.tsx`, and `InteractiveImage.tsx` to serialized optimized image descriptors and `client:visible`; preserve grid breakpoints, gallery selection/order, autoplay stopping, detail overlays, and fullscreen focus restoration.
- [x] 4.6 Adapt `BusinessCalendar.tsx` to a deterministic server fallback and `client:load` current-calendar/status updates every minute; reuse `data.ts` rules and show static weekly hours without JavaScript.

## 5. Implement Static Menus and Blog Routes

- [x] 5.1 Add shared `MenuContent.astro` and replace both menu pages with `.astro` routes, retaining category anchors, notices, dish cards, missing-image placeholders, layout-specific location/footer behavior, and existing styles.
- [x] 5.2 Add guarded 768px viewport forwarding that preserves category fragments, responsive height handling, and scrollspy tied to the menu's actual scrolling container; confirm direct visits and resize do not loop.
- [x] 5.3 Replace `DishDetailDrawer.tsx` with a styled native dialog and progressive activation for mobile cards; preserve image/name/description/features, backdrop/Close/Escape dismissal, focus trapping/restoration, and scroll position.
- [x] 5.4 Implement `src/pages/blog/[page].astro` with date-descending lists, 12 entries per page, opening summaries/dish labels/dates, five-number pagination, first/last boundaries, and a zero-article first-page state.
- [x] 5.5 Implement `src/pages/blog/[...slug].astro` and `src/layouts/BlogPost.astro`, retaining all existing public slugs, Markdown bodies, optional banners, six prefix-specific variants, generic fallback, AI disclosures, warnings, and restaurant conclusions.
- [x] 5.6 Replace `404.tsx` with the branded Astro not-found page and keep its home/blog/order/location recovery links functional.

## 6. Wire Metadata, Telemetry, and Artifact Consumers

- [x] 6.1 Add shared site metadata and `SEO.astro` with page-specific titles/descriptions/keywords, language, production canonical URLs, valid social tags, and absolute banner/fallback images in generated HTML.
- [x] 6.2 Configure sitemap generation to include all published article/listing routes and exclude redirect/not-found pages; verify robots, manifest, icon, and verification references match emitted files.
- [x] 6.3 Adapt `clarity.ts` for explicit browser-only initialization behind production mode and `PUBLIC_ENABLE_ANALYTICS`; preserve tracking identifiers/events/conversions and Google's DNT/path exclusions without preventing link navigation.
- [x] 6.4 Update source Azure host configuration for `/blog` forwarding and `/404.html` with a 404 response; avoid an SPA fallback and retain static deep-link compatibility.
- [x] 6.5 Modify `.github/workflows/test.yml` path filters and typecheck/build coverage for Astro/source assets/scripts; modify `.github/workflows/release.yml` analytics flag, size-report paths, `/dist` artifact source, and prebuilt upload configuration without executing publication.
- [x] 6.6 Update `scripts/indexnow.js` to read `dist/` child sitemap page URLs, exclude sitemap-index locations, and retain a network-free `--dry-run` mode.

## 7. Add Regression Coverage and Retire Gatsby

- [x] 7.1 Extend the existing Jest setup with focused cases for metadata validation, route conflicts, slug variants, deterministic date sorting, and pagination at 0/1/12/13/250 entries; retain business-hour boundary coverage.
- [x] 7.2 Add focused menu validation and analytics-policy cases covering invalid/duplicate YAML data, preserved item order, disabled/non-production tracking, DNT/exclusions, and navigation-independent event handling.
- [x] 7.3 Add a Node-built-in static-artifact check comparing generated routes/content counts against the baseline, sampling every article variant, and checking internal links, media, metadata, sitemap/host files, and absence of Gatsby artifacts.
- [x] 7.4 Remove migrated `.tsx` pages/templates, Gatsby entry/configuration/type files, and obsolete Gatsby/MDX/Helmet dependencies once replacements own all routes; regenerate the lockfile and confirm no active Gatsby imports remain.
- [x] 7.5 Update `README.md` and `docs/how-to-post.md` with Astro installation/dev/build/preview, `dist/` versus source `public/`, Markdown slug/date/banner conventions, YAML authoring, and analytics configuration.

## 8. Confirm the Migration Acceptance Contract

- [x] 8.1 Run `npm ci`, targeted existing/new Jest cases, `npm run typecheck`, and `npm run build` using the supported Node.js 22 version; resolve migration-caused errors without unrelated changes.
- [x] 8.2 Run the static-artifact check and verify all 250 current articles, 21 listing pages, final-page count of 10, unchanged public slugs, menu inventory, optional/Unicode banners, and source static files.
- [x] 8.3 Start local preview, confirm it responds, and request home, both menus, `/blog`, first/last lists, all article variants, media, and not-found output; separately confirm host redirect/404 policy rather than assume preview proves Azure behavior.
- [x] 8.4 Compare desktop/mobile screenshots and exercise navigation, category scrollspy, menu dialogs, gallery controls/autoplay/details, calendar refresh, reduced motion, and keyboard/focus states; fix migration regressions in a bounded comparison pass.
- [x] 8.5 Confirm JavaScript-disabled essential content and blocked/disabled analytics behavior; run IndexNow only with `--dry-run` and verify it contains page URLs rather than child sitemap XML URLs.
- [x] 8.6 Repeat the initial first-party JavaScript measurements under baseline conditions for home/menu/article; demonstrate lower bytes per route and absence of Gatsby/page-wide hydration before marking the performance requirement complete.
