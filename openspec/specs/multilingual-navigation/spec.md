## Purpose

Allow visitors to choose a supported reading language and remain in that language across Chengdu's statically published pages without losing their current content.

## Requirements

### Requirement: Supported languages and English defaults
The site SHALL support `en-US`, `es-MX`, `zh-CN`, and `vi`, with all four enabled when this change is complete. Unprefixed routes SHALL serve `en-US`. Other languages SHALL use the exact prefixes `/es-MX/`, `/zh-CN/`, and `/vi/`. Browser language and previously visited pages MUST NOT automatically redirect an unprefixed request away from English.

#### Scenario: Default language differs from the browser preference
- **WHEN** a browser configured for Spanish requests `/`
- **THEN** the site serves complete `en-US` content without an automatic language redirect

#### Scenario: Open a translated deep link
- **WHEN** a visitor directly requests `/es-MX/blog/how-to-make-fuqi-feipian/`
- **THEN** the delivered static HTML contains the Mexican Spanish article and document language `es-MX`

#### Scenario: Unsupported locale
- **WHEN** a visitor requests a locale prefix that the site does not support
- **THEN** the route is not generated and the static host returns its normal 404 behavior, not a successful English page

### Requirement: Equivalent-page language switching
Every localized page SHALL expose a language control with native language names and a textual current-language indication. Switching SHALL open the equivalent page by home/menu route, listing page number, or article slug rather than return to the home page. With JavaScript available, query parameters SHALL also be preserved, and fragments SHALL be preserved only when the target page contains the same anchor; otherwise they SHALL be omitted. Without JavaScript, equivalent-page navigation SHALL remain functional without requiring query or fragment preservation.

#### Scenario: Switch an article language
- **WHEN** a visitor on `/blog/how-to-make-fuqi-feipian/` chooses `vi`
- **THEN** the visitor reaches `/vi/blog/how-to-make-fuqi-feipian/` with the full Vietnamese article

#### Scenario: Switch a menu language
- **WHEN** a visitor on `/es-MX/menu-mobile/?source=visit#group-A` chooses `zh-CN`
- **THEN** the visitor reaches `/zh-CN/menu-mobile/?source=visit#group-A`

#### Scenario: Switch a listing page
- **WHEN** a visitor on `/zh-CN/blog/3/` chooses `en-US`
- **THEN** the visitor reaches `/blog/3/`, not the home page or first listing page

#### Scenario: Article heading anchor differs after translation
- **WHEN** a visitor switches languages from an article heading fragment that has no matching target anchor
- **THEN** the equivalent article opens without the invalid fragment

### Requirement: Accessible and progressively enhanced language control
The language control SHALL be available on initial desktop and mobile rendering, including the home-page hero, with localized accessible labels, visible keyboard focus, native language links, and a current-language indicator. It SHALL work without JavaScript. It MUST NOT require flags, hover-only discovery, or opening the mobile navigation overlay. At a 320px viewport and 200% zoom its choices SHALL remain readable and reachable without horizontal page overflow.

#### Scenario: Use the language control without scripts
- **WHEN** JavaScript is disabled and a visitor opens the language control and follows a language link
- **THEN** the browser navigates to the corresponding statically rendered localized page

#### Scenario: Use keyboard and assistive technology
- **WHEN** a visitor reaches the language control using the keyboard
- **THEN** the control, current language, and individual choices have meaningful labels and visible focus, and all choices can be activated without a pointer

### Requirement: Locale-preserving internal navigation
Home, menu, blog, article, pagination, location, and recovery links SHALL remain in the current language. Menu switching across the existing 768px breakpoint SHALL retain the locale, query string, and category fragment without redirect loops. External ordering, map, and telephone destinations SHALL retain their established values and behavior.

#### Scenario: Navigate from a translated article to the restaurant
- **WHEN** a reader on a `vi` article follows Visit Us
- **THEN** the link opens `/vi/#location` and does not discard the selected language

#### Scenario: Resize a localized menu
- **WHEN** `/es-MX/menu/?source=visit#group-A` crosses into the mobile breakpoint
- **THEN** it switches to `/es-MX/menu-mobile/?source=visit#group-A` without repeated redirects

### Requirement: Only complete languages are exposed
During incremental implementation the site SHALL expose only explicitly enabled languages. Enabling a language SHALL require complete interface, menu, and article translations. Disabled languages SHALL have no language-switcher choices, generated routes, alternate links, or sitemap entries. A missing enabled-language translation SHALL fail the build with a diagnostic instead of silently falling back to another language.

#### Scenario: Language is not yet ready during implementation
- **WHEN** `zh-CN` is disabled while its translations are being prepared
- **THEN** visitors are not offered `zh-CN` links or routes and crawlers are not told those pages exist

#### Scenario: Complete the requested change
- **WHEN** implementation is marked complete
- **THEN** all four languages are enabled and have the same complete visitor-facing page inventory
