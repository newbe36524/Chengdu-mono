## Purpose

Help visitors discover an enabled translation matching their browser preferences through a one-time, accessible suggestion that never changes languages without consent.

## Requirements

### Requirement: Ordered browser preference matching

With JavaScript available, the site SHALL consider the browser's ordered language preferences, falling back to its single language when the list is absent or empty. It SHALL select the first compatible enabled locale, comparing valid language tags case-insensitively. Exact supported tags SHALL match. Regional English, Spanish, and Vietnamese preferences SHALL match `en-US`, `es-MX`, and `vi` respectively. Chinese matching SHALL offer `zh-CN` for generic `zh`, explicit Simplified Chinese (`Hans`), and script-unspecified `zh-CN` or `zh-SG`; explicit Traditional Chinese (`Hant`) and script-unspecified `zh-TW`, `zh-HK`, or `zh-MO` SHALL NOT match Simplified Chinese. Invalid, unsupported, and disabled preferences SHALL be skipped.

#### Scenario: First compatible preference wins
- **WHEN** the browser preferences are `["fr-FR", "es-MX", "vi"]` and those last two locales are enabled
- **THEN** the selected suggestion is `es-MX`

#### Scenario: Regional language compatibility
- **WHEN** the browser prefers `es-ES`, `en-GB`, or `vi-VN`
- **THEN** the matching locale is `es-MX`, `en-US`, or `vi` respectively, if enabled

#### Scenario: Chinese script compatibility
- **WHEN** the browser prefers `zh-Hans`, `zh-SG`, `zh-Hant-CN`, or `zh-TW`
- **THEN** the first two match enabled `zh-CN` and the last two do not

#### Scenario: Single preference fallback
- **WHEN** the preference list is absent or empty and the browser's single language is `vi`
- **THEN** the matching locale is enabled `vi`

### Requirement: Eligible one-time suggestion

The site SHALL show at most one language suggestion per page initialization when no decision is recorded and the highest-priority compatible locale differs from the current document language. It SHALL support both unprefixed and translated pages. Unsupported preferences, disabled locales, or a best match equal to the current language SHALL produce no dialog, no navigation, and no recorded decision. Static content SHALL remain in the requested language before consent.

#### Scenario: Suggest a supported translation
- **WHEN** an undecided visitor with preference `es-MX` opens an English article
- **THEN** the English article remains rendered and a dialog offers its Spanish version

#### Scenario: Current language is already preferred
- **WHEN** preferences are `["en-US", "es-MX"]` and the page is English
- **THEN** no dialog is shown despite the secondary supported preference

#### Scenario: Unsupported or disabled language
- **WHEN** none of the browser preferences matches an enabled locale
- **THEN** the page remains unchanged without a dialog or recorded choice

#### Scenario: Translated deep link
- **WHEN** an undecided visitor preferring `vi` opens a Spanish article
- **THEN** the dialog offers the equivalent Vietnamese article without first redirecting

### Requirement: Explicit consent and equivalent-page navigation

The dialog SHALL offer explicit switch and stay actions. Switch SHALL navigate to the enabled locale's equivalent home, menu, listing page number, article slug, or recovery page, preserving query parameters. Fragments SHALL be retained only when known to exist in the destination; unverified or absent fragments SHALL be omitted. Stay and Escape dismissal SHALL retain the current URL and content. No browser preference or recorded decision SHALL automatically navigate on a later visit.

#### Scenario: Accept on an article
- **WHEN** a visitor on `/blog/how-to-make-fuqi-feipian/?source=visit` accepts Vietnamese
- **THEN** the destination is `/vi/blog/how-to-make-fuqi-feipian/?source=visit`

#### Scenario: Accept on a listing or menu
- **WHEN** a visitor accepts Chinese on `/blog/3/` or on `/menu-mobile/?source=visit#group-A` with a verified shared category anchor
- **THEN** navigation targets `/zh-CN/blog/3/` or `/zh-CN/menu-mobile/?source=visit#group-A`, not the homepage

#### Scenario: Unverified translated heading
- **WHEN** an accepted article translation has no verified counterpart to the current heading fragment
- **THEN** navigation preserves the equivalent article and query but omits the fragment

#### Scenario: Decline or dismiss
- **WHEN** the visitor selects stay or dismisses the dialog using Escape
- **THEN** the dialog closes without changing the page or URL

### Requirement: Persistent decision with safe storage failure behavior

Either switch, stay, or Escape dismissal SHALL record a browser-local decision before navigation or closure when persistent storage is available. A recorded decision SHALL suppress suggestions across subsequent routes and visits on the same origin regardless of later browser preferences. Opening the dialog alone SHALL NOT record a decision. Clearing storage SHALL permit another eligible suggestion. Read failures SHALL suppress the optional prompt without breaking the page; write failures SHALL respect the immediate visitor choice, suppress repeated prompts within that page, and emit an explicit diagnostic that cross-visit suppression could not be saved.

#### Scenario: Accepted choice persists
- **WHEN** a visitor accepts a suggestion and subsequently visits the translated page or an English URL
- **THEN** no further suggestion is shown and the requested URL is not automatically redirected

#### Scenario: Refused choice persists
- **WHEN** a visitor declines or dismisses and later reloads or visits another page
- **THEN** no suggestion is shown while the decision remains stored

#### Scenario: Viewing is not deciding
- **WHEN** a visitor leaves an open dialog by reloading without choosing
- **THEN** no decision has been saved and a subsequent eligible load can show it again

#### Scenario: Browser storage is unavailable
- **WHEN** browser policy prevents reading persistent storage
- **THEN** no suggestion opens, normal navigation remains usable, and the failure is diagnosed

#### Scenario: Persistence write fails
- **WHEN** saving a visitor's decision fails
- **THEN** their switch or stay choice still takes effect, the dialog does not reopen on that page, and a diagnostic identifies that later visits might prompt again

### Requirement: Accessible localized progressive enhancement

The dialog SHALL have a localized accessible title and description, native language names, meaningful button labels, visible keyboard focus, modal focus containment, and focus restoration on dismissal. The stay action SHALL receive initial focus. Dialog title, description, reminder, and stay text SHALL use the current page language; the switch action text SHALL use the target language's translation. Native language names SHALL be marked appropriately. At 320px width and 200% zoom, all content and actions SHALL remain reachable without horizontal page overflow. With JavaScript disabled or modal support unavailable, the dialog SHALL remain closed and the existing language switcher SHALL remain functional.

#### Scenario: Keyboard operation
- **WHEN** the dialog opens and a visitor navigates using Tab and Escape
- **THEN** focus starts on stay, remains within the modal, and returns to the prior focus target when dismissed

#### Scenario: Localized dialog on a small viewport
- **WHEN** a visitor opens the dialog on an enabled-language page at narrow width or zoom
- **THEN** title, instructions, and actions use that page's language and remain readable and reachable

#### Scenario: No JavaScript
- **WHEN** a visitor loads a page with JavaScript disabled
- **THEN** no suggestion is visible, requested content is unchanged, and manual language links still work
