## 1. Browser Preference and Decision Policy

- [x] 1.1 Add `repos/chengdu/src/lib/browser-language.ts` with ordered, case-insensitive valid-tag matching against the existing enabled registry, exact-first matching, regional English/Spanish/Vietnamese compatibility, and the explicit Chinese script policy in the specification.
- [x] 1.2 Add the minimal testable decision-storage boundary using `chengdu.browser-language-prompt.decided.v1 = "1"`; diagnose expected storage exceptions, suppress on read failure, respect immediate choices on write failure, and propagate unexpected errors.
- [x] 1.3 Add `src/lib/browser-language.test.ts` using existing Jest for preference ordering, empty-list fallback, malformed tags, case variations, regional variants, Chinese script precedence, disabled locales, current-language suppression, and no-match behavior.
- [x] 1.4 Cover acknowledged/unacknowledged state, no writes on display, acceptance/refusal/dismissal persistence, save-before-navigation ordering, repeated-handler guards, and expected versus unexpected storage failures using injected test doubles.

## 2. Localized Dialog and Shared Integration

- [x] 2.1 Add complete `language.prompt.*` copy and identical placeholders to `src/i18n/en-US.ts`, `es-MX.ts`, `zh-CN.ts`, and `vi.ts`; extend `src/lib/i18n.test.ts` for completeness and interpolated labels.
- [x] 2.2 Create `src/components/BrowserLanguagePrompt.astro` with one initially closed native dialog, current-page localized title/description, appropriately marked native language names, and pre-rendered candidate destinations using `localizedPagePathname`.
- [x] 2.3 Create `BrowserLanguagePrompt.module.css` using the incumbent warm/red palette, visible focus, fluid viewport gutters, scrollable content, wrapping labels, reachable action sizes, and stacked actions on narrow screens without added motion.
- [x] 2.4 Mount the prompt once in `src/layouts/Layout.astro` with `locale` and `currentPageIdentity`, independent of top-navigation visibility and without changing the existing manual language switcher or static metadata.
- [x] 2.5 Wire guarded client initialization, browser preference fallback, stored-decision checks, unsupported/current-language suppression, and native-dialog capability detection; defer while another native modal is open and recheck before display.
- [x] 2.6 Route switch, stay, and Escape through a single guarded decision handler; persist before navigation/closure, initially focus stay, restore prior connected focus after refusal, and close without navigation when another tab records a decision.

## 3. Equivalent-Page URL Handling

- [x] 3.1 Reuse `localizedPagePathname` and `preserveUrlState` to preserve home/menu/listing/article/recovery identity and live query parameters on acceptance.
- [x] 3.2 Identify guaranteed shared layout/menu anchors from the existing markup and category data; preserve only verified destination anchors, omit unverified translated heading fragments, and handle malformed fragment encoding narrowly.
- [x] 3.3 Add targeted coverage for translated deep links, listing page numbers, menu variants, recovery paths, query strings, shared category fragments, unknown fragments, and malformed fragments; retain existing menu breakpoint behavior.

## 4. Maintainer and Design Documentation

- [x] 4.1 Update `README.md` and `PRODUCT.md` to distinguish consent-based suggestions from prohibited automatic redirects and document preference matching, enabled-language configuration, the storage key, and persistence limits.
- [x] 4.2 Update `DESIGN.md` and `.impeccable/design.json` together to describe the new modal, incumbent token reuse, localized states, responsive controls, and keyboard interaction.

## 5. Implementation Acceptance

- [x] 5.1 Run the existing targeted Jest command from `repos/chengdu`: `npm test -- --runInBand src/lib/browser-language.test.ts src/lib/i18n.test.ts`; resolve failures related to this change.
- [x] 5.2 Run existing `npm run typecheck` and `npm run build`; inspect generated markup for a closed dialog, correct document language, unchanged canonical routes, and enabled-only candidate links.
- [x] 5.3 Exercise fresh-storage acceptance, refusal, Escape, reloads, later routes, cleared storage, changed browser preferences, duplicate initialization, cross-tab acknowledgment, and storage failures in the existing preview/browser tooling.
- [x] 5.4 Exercise no-JavaScript/manual switching, unavailable modal support, translated deep links, menu breakpoint transitions, shared and missing fragments, and coexistence with gallery/menu dialogs without automatic navigation or broken page interactions.
- [ ] 5.5 Exercise keyboard focus containment/restoration, accessible localized labels in all four languages, 320px viewport and 200% zoom, visible focus, long language names, and reachable actions; record any tooling limitation rather than claim unperformed acceptance.
  - Headless Firefox/WebDriver enforced a minimum 500px CSS viewport even when a 320px window was requested. WebDriver keyboard input did not change page zoom (devicePixelRatio remained 1), so 320px and 200% zoom acceptance remain unverified; focus, labels, wrapping, focus restoration, and action reachability were exercised at available sizes.
