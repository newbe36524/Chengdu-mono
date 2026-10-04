## Purpose

Provide comfortable, consistent light and dark presentation across Chengdu's static pages, automatically adapt the initial view to browser preferences, and remember an accessible manual theme choice.

## Requirements

### Requirement: Consistent light and dark presentation
The site SHALL offer light and dark themes across homepage content, navigation and language controls, both menu layouts, dish and gallery dialogs, calendar, floating actions, article listings and bodies, location/footer content, policy pages, and recovery pages in every enabled locale. Light mode SHALL preserve the existing visual identity and layout. Dark mode SHALL use coordinated dark surfaces and readable text, borders, focus indicators, and selected/hover states while preserving photography, branding, ordering links, content, responsive routing, and native interaction behavior. Normal text SHALL have at least 4.5:1 contrast, large text at least 3:1, and essential control boundaries and focus indicators at least 3:1 against adjacent colors.

#### Scenario: Browse representative dark surfaces
- **WHEN** a visitor uses dark mode on home, desktop/mobile menu, listing, article, policy, and recovery routes
- **THEN** first-party content and controls use coherent theme colors, including opened overlays, dialogs, placeholders, and dynamically inserted reviews
- **AND** text and essential control indicators meet the specified contrast thresholds

#### Scenario: Preserve intentional colors and imagery
- **WHEN** the visitor switches between light and dark modes
- **THEN** photographs, the already-dark hero, and provider logos are not inverted or recolored
- **AND** required provider attribution remains legible, and restaurant content and ordering destinations do not change

#### Scenario: Return to light
- **WHEN** a dark-mode visitor switches to light
- **THEN** the site's existing light palette and responsive layout are restored without persistent dark-only overrides

### Requirement: Resolve the theme before first paint
On each JavaScript-enabled page load, the site SHALL apply a valid saved explicit theme before the first visible content paint. Without a valid saved choice, it SHALL use the browser/system `prefers-color-scheme` preference, selecting dark when dark is preferred and light otherwise. Invalid stored values SHALL be treated as no saved choice. Unavailable storage SHALL not block preference resolution, and an unavailable color-preference API SHALL fall back to light. Automatic defaults MUST NOT be persisted as explicit choices.

#### Scenario: First visit with a dark preference
- **WHEN** a visitor with no saved theme directly loads a page while the system prefers dark
- **THEN** the first visible frame uses dark mode without a light-content flash
- **AND** no explicit theme preference is written

#### Scenario: First visit with a light or unavailable preference
- **WHEN** a visitor has no saved theme and prefers light or the color-preference API is unavailable
- **THEN** the first visible frame uses light mode

#### Scenario: Saved choice overrides the system
- **WHEN** a visitor loads any site route with a saved light choice and a dark system preference, or a saved dark choice and a light system preference
- **THEN** the first visible frame uses the saved choice

#### Scenario: Invalid or unreadable preference
- **WHEN** stored theme data is invalid or browser storage access fails
- **THEN** the initial theme follows the available system preference instead of failing initialization
- **AND** actual storage access failures produce a diagnostic without blocking content

### Requirement: Accessible manual theme switching
The site SHALL provide a localized two-state theme button in shared desktop and mobile navigation and on the mobile homepage's initially visible hero. It SHALL be reachable without opening the mobile menu, retain a stable accessible name and an accurate pressed state indicating whether dark mode is active, expose a textual state, support Enter and Space, and preserve keyboard focus when activated. All visible instances SHALL reflect the same effective theme. At 320px width and 200% zoom, theme and language controls SHALL remain readable and reachable without horizontal page overflow or overlap with ordering actions. Switching SHALL update the current page immediately without reload, URL changes, or required color-transition animation.

#### Scenario: Switch from the mobile hero
- **WHEN** a visitor opens the mobile homepage with navigation hidden at the top
- **THEN** a theme button is available on the hero without scrolling or opening an overlay
- **AND** its state agrees with the navigation button when navigation becomes visible

#### Scenario: Activate with the keyboard
- **WHEN** a keyboard visitor focuses a theme button and activates it with Enter or Space
- **THEN** the opposite theme is applied, focus remains on the button, and every theme button reports the updated state

#### Scenario: Use another enabled locale or a narrow viewport
- **WHEN** a visitor uses the theme control in any enabled locale at 320px width or 200% zoom
- **THEN** labels, state text, and announcements match the page language and the controls remain usable without page overflow

### Requirement: Persist explicit theme choices safely
Each explicit user selection SHALL be stored locally for later same-origin visits, reloads, direct links, and language/page navigation. Only light or dark SHALL be accepted as saved choices. Changing system appearance during an already-open page SHALL not overwrite its effective theme; an unsaved automatic choice SHALL be reevaluated on the next page load. If persistence fails, switching SHALL still succeed on the current page, and the site SHALL announce in the page language that the choice could not be saved. Preference access MUST NOT require accounts, network requests, cookies, analytics consent, or storing unrelated user data.

#### Scenario: Restore a manual preference
- **WHEN** a visitor manually chooses a theme, then reloads or navigates to another same-origin route or locale
- **THEN** the chosen theme is restored before visible rendering regardless of system appearance

#### Scenario: Storage write is blocked
- **WHEN** a visitor activates the toggle but local storage rejects the write
- **THEN** the new theme remains active and all current-page buttons agree
- **AND** a localized accessible status message explains that the choice was not saved

#### Scenario: System appearance changes during a session
- **WHEN** system appearance changes after the current page has loaded
- **THEN** the current page keeps its theme
- **AND** the next page load honors a saved explicit choice or reevaluates system appearance when no choice is saved

### Requirement: Progressive enhancement preserves essential content
When JavaScript is disabled, the site SHALL keep essential content, language links, menu navigation, and ordering links usable and SHALL provide system-based theme adaptation through CSS where the browser supports it. An inoperative manual theme control MUST NOT be presented as usable. Persisted browser storage preferences are not required to be read when JavaScript is disabled.

#### Scenario: Browse without JavaScript
- **WHEN** a visitor disables JavaScript and opens home, menu, or article content
- **THEN** static content and essential links remain available, CSS follows the supported system color preference, and inactive manual theme controls are hidden
