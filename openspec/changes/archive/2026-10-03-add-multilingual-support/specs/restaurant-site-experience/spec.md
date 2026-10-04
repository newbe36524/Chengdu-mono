## MODIFIED Requirements

### Requirement: Preserve the restaurant home presentation
The site SHALL retain the home page's restaurant identity, responsive video hero, delivery/pickup/menu actions, featured dishes, restaurant features, gallery, about text, location section, and footer in every enabled language. Existing red/gold styling, fonts with suitable language fallbacks, dish images, translated image descriptions, and translated AI image labels MUST remain recognizable at desktop and mobile sizes. English SHALL remain at `/`; non-English home pages SHALL use `/{locale}/`.

#### Scenario: Browse the home page on desktop or mobile
- **WHEN** a visitor opens `/` or an enabled locale's home page at a desktop or mobile viewport
- **THEN** the existing sections, equivalent localized copy, media, language control, and ordering actions are presented in their established order without clipped controls or horizontal page overflow

#### Scenario: Video playback is unavailable
- **WHEN** a browser cannot autoplay or load the background video
- **THEN** the restaurant title, hero layout, language control, and action links remain visible and usable

### Requirement: Preserve navigation and ordering destinations
The site SHALL expose localized equivalents of Home, Full Menu, Get Delivery, Get Pickup, Blogs, and Visit Us navigation, retain mobile navigation and contextual floating actions, and preserve the destinations and new-tab behavior of existing ordering links. Internal links SHALL retain the selected language. Ordering MUST remain available regardless of the displayed business-hour state.

#### Scenario: Open the full menu from navigation
- **WHEN** a visitor follows Full Menu below the 768px breakpoint or at a desktop viewport
- **THEN** the visitor can reach the corresponding same-language mobile or desktop menu without a redirect loop

#### Scenario: Follow ordering links without analytics
- **WHEN** analytics are unavailable, blocked, or disabled and a visitor selects pickup or delivery in any language
- **THEN** the normal link opens the existing MealKeyway or DoorDash destination without waiting for tracking

#### Scenario: Visit location from the mobile menu
- **WHEN** a visitor selects Visit Us on a page without a local location section
- **THEN** the link reaches the selected language's home page location section rather than an absent fragment

### Requirement: Preserve desktop and mobile menu browsing
The site SHALL retain `/menu` and `/menu-mobile` as English menus and provide both equivalents under each enabled locale prefix. It SHALL retain alphabetically ordered category prefixes, original item order, menu-update notices, dish images, and image-less placeholders showing the dish code and localized name. Category names and introductions, item names, descriptions, feature badges, and accessible control labels SHALL use the page language. English names and introductions and source bilingual fields MUST NOT be deleted; cultural Chinese names retained as secondary labels SHALL be marked with their own language.

#### Scenario: Select and scroll through a menu category
- **WHEN** a visitor selects a category or scrolls the menu's content area in any language
- **THEN** the corresponding group can be reached and the active category indicator follows the visible group

#### Scenario: A dish has no image
- **WHEN** a menu item lacks a matching image asset
- **THEN** its code and localized name remain visible in a deliberate placeholder rather than a broken image or a missing card

#### Scenario: Resize or directly open either menu URL
- **WHEN** either menu route is opened directly or the viewport crosses 768px
- **THEN** menu content remains reachable in the same language with query parameters and category fragments preserved, and the visitor receives the appropriate responsive presentation without repeated redirects

#### Scenario: Open localized dish details
- **WHEN** a visitor activates a mobile menu dish card on a translated page
- **THEN** the drawer shows the localized name, description, feature badges, and close label while retaining existing modal keyboard and focus behavior

### Requirement: Preserve contact information and live business hours
The site SHALL retain the restaurant address, both telephone links, map embed, weekly business-hour schedule, current-month calendar, current-day marker, open-status labels, and next-opening message. Dates, weekday labels, time presentation, status labels, and next-opening duration messages SHALL use the selected language. Runtime status SHALL be calculated from the visitor's current local clock using existing business rules and refreshed at least once per minute; generated HTML MUST NOT present a build-time status as a live value. Changing language MUST NOT alter schedule values or status calculations.

#### Scenario: Open the site after the build date
- **WHEN** a visitor loads a localized site on a later date or during a different open/closed period
- **THEN** the calendar and localized status update to the visitor's current date and time rather than remain frozen at build time

#### Scenario: Reach an opening or closing boundary
- **WHEN** local time reaches 11:00, a weekday 21:45 closing, or a weekend 22:00 closing
- **THEN** the localized displayed state follows the existing inclusive-opening and exclusive-closing rules within one refresh interval

#### Scenario: Compare hours across languages
- **WHEN** the same runtime instant is displayed in two enabled languages
- **THEN** the labels and formatting differ by locale but contact values, weekly schedule, current status, and next-opening instant are equivalent
