## 1. Configuration and provider types

- [x] 1.1 Add the supplied listing URL as `site.googleReviewsUrl` in `src/lib/site.ts`, preserving `site.mapUrl` and every existing ordering destination.
- [x] 1.2 Define the three public review settings in `src/env.d.ts` and implement side-effect-free validation in `src/lib/google-reviews.ts`: default off, literal `true` enables, and enabled missing/blank key or Place ID fails without printing values.
- [x] 1.3 Add `@types/google.maps` as a locked development dependency using the existing package manager; confirm current `Place`, `Review` and attribution definitions without adding a widget or runtime loader package.
- [x] 1.4 Pass the three optional `vars.PUBLIC_*` review settings into the existing production build step and update `tools/github-pages-workflow.test.js`, preserving analytics enablement, existing workflow permissions, triggers and publication logic.

## 2. Static section and policy surfaces

- [x] 2.1 Create `src/components/GoogleReviews.astro` with a labeled section, static heading, permanent safe new-tab Maps anchor, off/pending status, no-JavaScript fallback, result templates and one polite status region; do not serialize unused configuration when disabled.
- [x] 2.2 Compose the component in `src/pages/index.astro` after `#your-table` and before `#about`, retaining all existing content, relative section order, motion behavior and floating-action clearance.
- [x] 2.3 Create `src/components/GoogleReviews.module.css` using the existing section/container conventions and warm red-and-gold system; provide one/two/three-column layouts, wrapped text, visible focus, accessible numeric ratings and usable full-text expansion without autoplay.
- [x] 2.4 Obtain the official unmodified Google Maps attribution SVG as `public/google-maps-logo.svg`, record the official source, and render it with required clear space, legibility and accessible alternative text wherever API-derived data is displayed.
- [x] 2.5 Add static `/privacy/` and `/terms/` pages with accurate review-loading disclosures and applicable Google policy references, without making unverified legal claims; add footer links while preserving existing links.

## 3. Browser loading and safe review presentation

- [x] 3.1 Implement a scoped browser initializer and one memoized asynchronous Google Maps SDK load in `src/lib/google-reviews.ts`; load only Places on demand, use official types, and keep imports free of browser side effects.
- [x] 3.2 Observe the enabled section with a 200px loading boundary, initiate once on visibility, fall back to one initialization attempt when observation is unsupported, and ensure disabled/unrelated routes do not load the provider.
- [x] 3.3 Fetch `displayName`, `formattedAddress`, `rating`, `userRatingCount` and `reviews` for the configured verified Place ID exactly once; preserve provider review order and identify the set as Google-selected rather than latest or complete.
- [x] 3.4 Implement the total 10-second SDK-plus-data deadline, sanitized script/auth/request failure reporting, explicit success/empty/unavailable states, terminal-state guard against late responses, and observer/timer cleanup without polling or automatic retries.
- [x] 3.5 Validate aggregate fields independently, require returned author attribution for displayed reviews, handle missing optional fields and rating-only entries truthfully, and distinguish a genuinely empty result from a nonempty unusable response.
- [x] 3.6 Render review text and attribution through safe DOM APIs, preserve full returned text and valid publication dates, validate HTTPS author/provider links, display required provider attribution, and add no application persistence or review snapshots.

## 4. Automated behavior and static-output coverage

- [x] 4.1 Add Jest cases in `src/lib/google-reviews.test.ts` for off/complete/incomplete configuration, provider-order preservation, aggregate-versus-sample distinction, missing optional fields, missing authors, rating-only reviews and full long-text availability.
- [x] 4.2 Add mocked browser/provider cases with existing Jest facilities for deferred loading, repeated viewport entries, one details request, unsupported observation, all terminal states, SDK/auth/request failures, deadline expiry, ignored late responses, cleanup and unchanged Maps-link/focus behavior.
- [x] 4.3 Cover inert markup-like review text, rejected unsafe links, attribution presence and sanitized diagnostics; assert review content is not written to persistent browser storage or static snapshots.
- [ ] 4.4 Extend `tools/check-static-artifacts.js` with exactly the two policy-route/sitemap additions, generated policy/footer links, review placement, permanent Maps fallback and attribution asset assertions, retaining all baseline article/menu/route checks and leaving the historical baseline untouched. **Blocked:** rerun the final artifact assertions after static generation is available.
- [x] 4.5 Run the related selectors in one invocation from `repos/chengdu`: `npm test -- --runInBand --runTestsByPath src/lib/google-reviews.test.ts tools/github-pages-workflow.test.js`; resolve any failures caused by this change.
- [ ] 4.6 Run `npm run typecheck`, then a default-off `npm run build` and `node tools/check-static-artifacts.js`; confirm intentional output-route changes, unchanged article/menu content and no review-data requests during generation. **Blocked:** the current locale work fails prerendering `/blog/how-to-make-ant-climbing-tree/` with `Cannot read properties of undefined (reading 'replace')`.
- [x] 4.7 Exercise enabled builds with noncredential test configuration without browsing against Google, plus missing/blank-setting failure cases; confirm offline Places-independent generation and no invented review values or server secrets in delivered HTML/assets.

## 5. Documentation and browser acceptance

- [x] 5.1 Update `README.md` with all settings, matching repository-variable names, browser-key exposure/restrictions, billing and quota prerequisites, correct-business Place ID verification, policy review, limited review selection, disabled/error behavior and lack of persistent review storage.
- [x] 5.2 Update `DESIGN.md` and `.impeccable/design.json` together to record the intentional review-section extension without changing unrelated product claims or visual rules.
- [ ] 5.3 Use the existing local preview to inspect desktop and 320px mobile layouts with mocked success, empty, unavailable and disabled states; verify full text, keyboard focus/links, 200% text zoom, no-JavaScript fallback, reduced motion and unblocked ordering/location access. **Blocked:** the concurrent locale work currently causes static generation to fail on `/blog/how-to-make-ant-climbing-tree/`; full preview acceptance must be rerun after that build blocker is resolved.
- [x] 5.4 Inspect review-specific network activity before visibility, after visibility and on unrelated routes; confirm one details request per page, no polling, no early SDK loading and no review-provider traffic when disabled, independently of existing fonts/map/analytics.
- [ ] 5.5 When authorized restricted configuration and a verified Place ID are supplied, validate a real preview against the intended CHENGDU listing, actual rating/count/reviews and complete visible attribution; if unavailable, record this acceptance step as blocked rather than claiming mocked data proves live integration. **Blocked:** no authorized restricted browser key or verified API Place ID was supplied.
