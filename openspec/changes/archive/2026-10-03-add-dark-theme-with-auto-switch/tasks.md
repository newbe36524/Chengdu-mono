## 1. Theme Foundation and First Paint

- [x] 1.1 Inventory color roles in the owning files listed in `design.md`; record the existing light values and intentional fixed-color hero, photo overlays, CTAs, footer, and provider attribution before replacing declarations.
- [x] 1.2 Add semantic light/dark tokens to `repos/chengdu/src/styles/global.css`, including body/paragraph/heading ink, menu canvas, warm surfaces, border/focus/selected/hover roles, and warning/calendar states; keep light defaults unchanged and provide explicit-theme precedence, CSS-only system fallback, and native `color-scheme`.
- [x] 1.3 Add the standalone `src/lib/theme-bootstrap.js` resolver accepting only `light`/`dark` from `chengdu-theme`, falling back to system preference then light, with narrow storage-failure diagnostics and no write on automatic resolution.
- [x] 1.4 Inline the raw bootstrap in `src/layouts/Layout.astro` before styles; inspect generated HTML ordering rather than relying on source ordering, and keep initialization independent of analytics and homepage-only scripts.

## 2. Accessible Switching and Persistence

- [x] 2.1 Add `src/lib/theme.ts` for typed explicit theme selection, root-attribute updates, synchronization of all control instances, and local persistence; preserve the current page theme on write failure and surface a diagnostic.
- [x] 2.2 Add `src/components/ThemeToggle.astro` using a native button, stable localized accessible name, accurate `aria-pressed`, sun/moon state icons, focus styling, and hidden-until-bound progressive enhancement; integrate one shared localized polite status region and clear prior failure feedback after successful persistence.
- [x] 2.3 Add complete toggle/state/persistence-feedback messages to `src/i18n/en-US.ts`, `es-MX.ts`, `zh-CN.ts`, and `vi.ts` using the existing message-key conventions.
- [x] 2.4 Integrate the toggle beside the language/menu controls in `TopNavigation.astro` and in a mobile hero utility row in `HomePage.astro`; reuse `LanguageSwitcher` in that row and keep both controls initially reachable while the mobile header is hidden.
- [x] 2.5 Adjust only the necessary navigation/hero sizing rules for narrow widths and zoom, preserving brand accessibility, mobile overlay focus handling, existing header behavior, and menu panes' measured-header clearance.

## 3. Apply the Theme Across Existing Surfaces

- [x] 3.1 Replace theme-sensitive colors in navigation and language CSS Modules, including translucent header surfaces, hamburger/close controls, dropdowns, mobile panels, links, and hover/focus states.
- [x] 3.2 Tokenize homepage section/card colors in `index.module.css`, `IndexSection.module.css`, `RestaurantFeatures.module.css`, and `GoogleReviews.module.css`; theme inserted review content and retain the unmodified Google logo on a legible fixed-light attribution backing with required clear space.
- [x] 3.3 Update affected gallery/image/drawer CSS Modules and opened-dialog states without inverting photographs, recoloring intentional dark overlays, or changing native keyboard/focus behavior.
- [x] 3.4 Theme `menu.module.css`, `menu-mobile.module.css`, and scoped rules in `MenuContent.astro`, including active categories, search controls, notices, missing-image placeholders, and dish dialogs; preserve category history and responsive route switching.
- [x] 3.5 Theme location/calendar/action-bar surfaces and state pairs in their owning modules; retain readable intentional footer/CTA colors and preserve maps, business-hour behavior, safe-area clearance, and ordering destinations.
- [x] 3.6 Theme `src/templates/blog-list.module.css` and `blog-post.module.css`, including prose, metadata, notices, pagination, action links, and hover/focus states; retain article variants and existing reduced-motion behavior.
- [x] 3.7 Replace theme-sensitive scoped policy colors in English/localized privacy and terms pages, and theme recovery surfaces in `404.module.css`; verify direct links and locale-specific rendering use the shared initialization.

## 4. Automated Coverage and Static Delivery

- [x] 4.1 Add `src/lib/theme.test.ts` in the existing Jest runner; execute the actual bootstrap with Node VM and cover absent/invalid/valid saved values, both system modes, missing `matchMedia`, storage-access exceptions, saved-choice precedence, and zero automatic writes.
- [x] 4.2 Cover explicit-choice persistence, duplicate-button synchronization, accurate pressed/text state, write-failure diagnostics/status, warning clearing after a later successful write, and preservation of the current theme using small DOM/storage fakes rather than a new testing dependency.
- [x] 4.3 Extend `tools/check-static-artifacts.js` to inspect bootstrap presence and ordering, native localized control markup, and mobile hero entry across representative generated routes while retaining existing static-content, no-React, and route-specific script checks.
- [x] 4.4 From `repos/chengdu`, run `npm test -- --runInBand src/lib/theme.test.ts src/lib/i18n.test.ts`, `npm run typecheck`, `npm run build`, and `node tools/check-static-artifacts.js`; resolve failures directly caused by the theme work.
- [x] 4.5 Measure representative home/menu/article initial first-party script transfers against the existing static-delivery baselines, reporting third-party traffic separately and preserving the runtime budgets rather than waiving them.

## 5. Browser Acceptance and Documentation

- [x] 5.1 Inspect cold direct loads under system light/dark and both opposite saved choices on home, desktop/mobile menu, listing, article, policy, and recovery pages; confirm the first visible content frame matches the resolved theme, then verify manual choice survives reload and same-origin locale/page navigation.
- [x] 5.2 Inspect desktop/mobile normal, hover, selected, keyboard-focus, open-overlay/dialog, placeholder, calendar, floating-action, and enabled-review states in both themes; measure text ratios of 4.5:1 (3:1 for large text) and essential boundary/focus ratios of 3:1, correcting theme-related contrast defects without changing imagery.
- [x] 5.3 Check all enabled locale labels at 320px width and 200% zoom, Enter/Space activation and retained focus, synchronized hero/header controls, read/write storage failures, no-JavaScript system-theme fallback with inactive toggles hidden, and reduced-motion behavior; ensure no control overlaps or horizontal page overflow.
- [x] 5.4 Update `README.md` with load-time system adaptation, explicit-choice precedence, local storage behavior/failure feedback, and no-JavaScript limits; update `DESIGN.md` and `.impeccable/design.json` together with final semantic tokens and light/dark control previews.
