## Purpose

Preserve Chengdu's restaurant discovery and ordering experience across desktop and mobile while moving presentation to static pages and retaining localized interactions.

## ADDED Requirements

### Requirement: Preserve the restaurant home presentation
The site SHALL retain the home page's restaurant identity, responsive video hero, delivery/pickup/menu actions, featured dishes, restaurant features, gallery, about text, location section, and footer. Existing red/gold styling, fonts, dish images, image descriptions, and AI image labels MUST remain recognizable at desktop and mobile sizes.

#### Scenario: Browse the home page on desktop or mobile
- **WHEN** a visitor opens `/` at a desktop or mobile viewport
- **THEN** the existing sections, copy, media, and ordering actions are presented in their established order without clipped controls or horizontal page overflow

#### Scenario: Video playback is unavailable
- **WHEN** a browser cannot autoplay or load the background video
- **THEN** the restaurant title, hero layout, and action links remain visible and usable

### Requirement: Preserve navigation and ordering destinations
The site SHALL expose Home, Full Menu, Get Delivery, Get Pickup, Blogs, and Visit Us navigation, retain mobile navigation and contextual floating actions, and preserve the destinations and new-tab behavior of existing ordering links. Ordering MUST remain available regardless of the displayed business-hour state.

#### Scenario: Open the full menu from navigation
- **WHEN** a visitor follows Full Menu below the 768px breakpoint or at a desktop viewport
- **THEN** the visitor can reach the corresponding mobile or desktop menu without a redirect loop

#### Scenario: Follow ordering links without analytics
- **WHEN** analytics are unavailable, blocked, or disabled and a visitor selects pickup or delivery
- **THEN** the normal link opens the existing MealKeyway or DoorDash destination without waiting for tracking

#### Scenario: Visit location from the mobile menu
- **WHEN** a visitor selects Visit Us on a page without a local location section
- **THEN** the link reaches the home page location section rather than an absent fragment

### Requirement: Preserve desktop and mobile menu browsing
The site SHALL retain `/menu` and `/menu-mobile`, alphabetically ordered category prefixes, original item order, English names and introductions, menu-update notices, dish images, and image-less placeholders showing the dish code and name. Mobile cards SHALL expose existing dish descriptions and feature badges. Source bilingual fields MUST NOT be deleted during migration.

#### Scenario: Select and scroll through a menu category
- **WHEN** a visitor selects a category or scrolls the menu's content area
- **THEN** the corresponding group can be reached and the active category indicator follows the visible group

#### Scenario: A dish has no image
- **WHEN** a menu item lacks a matching image asset
- **THEN** its code and name remain visible in a deliberate placeholder rather than a broken image or a missing card

#### Scenario: Resize or directly open either menu URL
- **WHEN** either menu route is opened directly or the viewport crosses 768px
- **THEN** menu content remains reachable and the visitor receives the appropriate responsive presentation without repeated redirects

### Requirement: Preserve gallery and dish detail interactions
The site SHALL retain featured-image detail expansion and the gallery's responsive grid, previous/next controls, autoplay behavior, and fullscreen dish information. Mobile menu dish selection SHALL open a detail drawer with image, name, description, and feature badges.

#### Scenario: Interact with the gallery
- **WHEN** a visitor uses previous navigation or expands a gallery image on mobile
- **THEN** the appropriate slide/detail state is shown and autoplay stops as in the existing interaction

#### Scenario: Open and close dish information with a keyboard
- **WHEN** a visitor activates a dish detail control with Enter or Space and closes the dialog with Escape or Close
- **THEN** its details are readable, focus stays within the open dialog, background scrolling is prevented, and closing restores focus to the initiating control

#### Scenario: Close an overlay from its backdrop
- **WHEN** a visitor selects the backdrop outside an open dish dialog
- **THEN** the dialog closes without activating a background card or losing the current browsing position

### Requirement: Preserve contact information and live business hours
The site SHALL retain the restaurant address, both telephone links, map embed, weekly business-hour schedule, current-month calendar, current-day marker, open-status labels, and next-opening message. Runtime status SHALL be calculated from the visitor's current local clock using existing business rules and refreshed at least once per minute; generated HTML MUST NOT present a build-time status as a live value.

#### Scenario: Open the site after the build date
- **WHEN** a visitor loads the site on a later date or during a different open/closed period
- **THEN** the calendar and status update to the visitor's current date and time rather than remain frozen at build time

#### Scenario: Reach an opening or closing boundary
- **WHEN** local time reaches 11:00, a weekday 21:45 closing, or a weekend 22:00 closing
- **THEN** the displayed state follows the existing inclusive-opening and exclusive-closing rules within one refresh interval

### Requirement: Preserve essential content without client scripts
The site SHALL render navigation links, restaurant information, menu categories and dish names, article content, and ordering links in the delivered HTML. Localized enhancements MUST NOT make essential content depend on hydration or third-party availability.

#### Scenario: Browse with JavaScript disabled
- **WHEN** a visitor disables JavaScript
- **THEN** core pages, menu anchors, article links, weekly hours, and ordering destinations remain usable, even when dialogs, live status, or carousel motion are unavailable
