## 1. Assessment and Baseline

- [x] 1.1 Recheck React imports, TSX files, hydration directives, dependency/configuration references, and all callers under `repos/chengdu`; record each fragment's native replacement or concrete retention blocker in `docs/react-to-astro-migration.md`.
- [x] 1.2 Capture the current React/Astro baseline before editing: Node/browser versions, enabled locales, analytics/review flags, desktop/mobile screenshots, initial and post-gallery first-party JavaScript transfer, generated HTML/JavaScript and total artifact size, and median of three build durations; use identical conditions for the final comparison.
- [x] 1.3 Record existing parity cases from `restaurant-site-experience` and current source, including featured inline expansion, gallery playback, dialog focus/backdrop behavior, minute-based local-clock status, localization, and essential no-JavaScript content.

## 2. Native Featured Cards and Dish Details

- [x] 2.1 Replace `IndexSection.tsx` and `MainGallery.tsx` with same-basename Astro components, using a slot for section content and preserving section IDs, tone, locale, dish order, images, descriptions, badges, and loading metadata.
- [x] 2.2 Replace `InteractiveImage.tsx` with `InteractiveImage.astro`; implement featured-card inline expansion through a native activation button, `aria-expanded`/`aria-controls`, outside dismissal, Escape, and scrollable detail content without invalid nested controls.
- [x] 2.3 Implement grid-card fullscreen details with pre-rendered, uniquely labeled native dialogs; wire Close, Escape, backdrop hit detection, focus containment/restoration, exact body-overflow restoration, and a local bubbling expansion event.
- [x] 2.4 Adapt `InteractiveImage.module.css` only for changed native markup; preserve aspect ratios, AI notices, visible focus, reduced-motion rules, and usable unenhanced content; initialize each rendered card instance once.
- [x] 2.5 Add focused `InteractiveImage.test.js` checks using the existing Jest/VM pattern for expansion, independent instances, dismissal, modal cleanup, and gallery expansion notification.

## 3. Native Gallery Enhancement

- [x] 3.1 Replace `GridGallery.tsx` with Astro-rendered Swiper markup and scoped previous/next/playback controls; render localized dish labels during the build rather than passing a callback across the component boundary.
- [x] 3.2 Initialize the installed Swiper core and current modules through a visibility-gated dynamic import; preserve the two-row layout, 1.15/2/3 columns, spacing, breakpoints, non-looping navigation, touch behavior, localized A11y messages, and menu destination.
- [x] 3.3 Preserve 4.5-second autoplay, hover pause, persistent pause after focus/navigation/touch/expansion, explicit keyboard-operable Play, and reduced-motion changes; keep controls unavailable until initialization succeeds and the static gallery usable without scripts or after an initialization error.
- [x] 3.4 Update `Gallery.module.css` for native navigation markup and the pre-initialization fallback; clean up observers/listeners/Swiper on exit and reinitialize exactly once on back-forward-cache restoration.
- [x] 3.5 Add `GridGallery.test.js` coverage for one-time initialization, fallback behavior, responsive options, pause/play event ordering, dynamic reduced motion, detail expansion, and exit/restore lifecycle.

## 4. Native Business Calendar

- [x] 4.1 Replace `BusinessCalendar.tsx` with an Astro shell and immediate browser-local update using `data.ts`, existing locale messages, and `Intl`; retain current date/status, countdown pluralization, weekdays, month cells, today marker, and legend without emitting build-time live values.
- [x] 4.2 Refresh status at least every 60 seconds and date/month cells on rollover; clear the instance timer on exit and refresh/restart once on persisted restoration, retaining the static weekly-hours fallback in `LocationSection.astro`.
- [x] 4.3 Add `BusinessCalendar.test.js` and extend existing `data.test.ts` as needed for immediate initialization, minute refresh, 11:00 opening, weekday 21:45/weekend 22:00 closing, local timezone behavior, countdowns, leap-month/year rollover, and single-timer cleanup/restoration.

## 5. Integration and Runtime Removal

- [x] 5.1 Update `HomePage.astro` and `LocationSection.astro` to explicit native component imports, remove obsolete `client:visible`/`client:load`, and preserve shared default/enabled-locale rendering and unrelated reviews, content, ordering, and analytics behavior.
- [x] 5.2 Confirm all replacement components are wired and remove the five obsolete TSX files; resolve any tightly coupled type/import issues without changing business-hour data, image data, translations, or destinations.
- [x] 5.3 With no retained blocker, remove `react()` from `astro.config.mjs`, uninstall the five direct React integration/runtime/type packages with npm, and clean React-specific `tsconfig.json`/`jest.config.ts` settings while retaining Swiper and the existing commands. If a blocker remains, document its route/boundary/removal condition before preserving only the required React configuration.
- [x] 5.4 Extend `tools/check-static-artifacts.js` to assert native homepage content, absence of build-time live status, and absence of React hydration entries/runtime in the generated dependency graph for the zero-exception case; preserve existing route/content/feed/review checks and derive enabled-locale cases from current configuration where needed.

## 6. Regression and Measurement

- [x] 6.1 From `repos/chengdu`, run targeted coverage together with `npm test -- --runInBand src/components/InteractiveImage.test.js src/components/GridGallery.test.js src/components/BusinessCalendar.test.js src/components/data.test.ts src/components/DishImages.test.ts src/lib/i18n.test.ts`, then `npm run typecheck`, `npm run build`, and `node tools/check-static-artifacts.js`; address failures caused by this migration.
- [x] 6.2 Inspect desktop/mobile and 768px/1024px breakpoint behavior: same section order and imagery, featured expansion, previous/next and swipe, play/pause, reduced motion at load and on change, modal keyboard/focus/backdrop/scroll behavior, and no-JavaScript content with no inert-looking controls.
- [x] 6.3 Inspect default and currently enabled localized homepages for matching labels, alt text, dates, countdowns, menu destinations, and isolated enhancement initialization; confirm representative menu/article pages do not load homepage-only code and review/analytics flags still follow their existing contracts.
- [x] 6.4 Repeat the baseline measurement protocol; demonstrate lower cumulative first-party JavaScript through calendar initialization and gallery activation with no initial-transfer increase, report build-duration and artifact-size changes, and separate third-party traffic. If targets are missed, adjust the native implementation and repeat the same comparison before declaring completion.

## 7. Documentation and Completion

- [x] 7.1 Finalize `docs/react-to-astro-migration.md` with all assessed fragments, replacement ownership, reproducible measurement conditions/results, and either explicit zero exceptions or the technical reason, routes, boundary, and removal strategy for every retained fragment.
- [x] 7.2 Update `README.md`, `PRODUCT.md`, and framework/interaction facts in `DESIGN.md`; refresh its `.impeccable/design.json` companion where changed markup/metadata requires it, without introducing a redesign.
- [x] 7.3 Reconcile the final implementation against the runtime delta and existing restaurant behavior contract: no reachable React runtime in the zero-exception case, preserved essential static content, equivalent interactive behavior, and documented maintenance boundaries.
