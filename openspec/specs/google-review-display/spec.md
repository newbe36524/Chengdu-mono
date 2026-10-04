## Purpose

Help prospective Chengdu diners read authentic, attributed Google customer feedback on the homepage while preserving a useful experience when the external provider is unavailable.

## Requirements

### Requirement: Retrieve only the intended business through a supported source
The reviews feature SHALL use an official Google Maps Platform interface and a verified Place ID for CHENGDU at 6620 S Memorial Dr, Tulsa, OK 74133, corresponding to the business listing supplied in the change description. It MUST NOT scrape Google Maps, infer an API Place ID from the URL's hexadecimal identifiers, or introduce fabricated production reviews. The display SHALL identify the returned reviews as a limited Google-selected set rather than all reviews or the latest reviews.

#### Scenario: Retrieve reviews for the configured restaurant
- **WHEN** the enabled feature retrieves a successful response for the verified business
- **THEN** it displays at most five returned reviews in provider order, without filtering by sentiment or substituting hand-authored testimonials

#### Scenario: Explain the limited review selection
- **WHEN** returned reviews are displayed
- **THEN** nearby text explains that they are a selection returned by Google and a link allows visitors to view more reviews on Google Maps

### Requirement: Enable live reviews only with complete public configuration
Live review loading SHALL be disabled unless explicitly enabled by build configuration. Enabled builds MUST reject missing or blank browser API key and Place ID settings with actionable diagnostics. The browser key SHALL be documented as publicly visible and subject to HTTP-referrer and API restrictions; server-side credentials MUST NOT be included in delivered assets. The existing production build configuration SHALL accept the same optional settings as local builds, independently of analytics configuration.

#### Scenario: Build with reviews disabled
- **WHEN** a build does not explicitly enable live reviews
- **THEN** the homepage includes the reviews heading and Google Maps link, shows no sample rating or testimonial, and starts no review-provider request

#### Scenario: Build with incomplete enabled configuration
- **WHEN** live reviews are explicitly enabled but the browser key or Place ID is missing or blank
- **THEN** the build fails with a diagnostic identifying the missing setting without exposing credential values

#### Scenario: Enable reviews with analytics disabled
- **WHEN** reviews are configured and enabled while analytics remain disabled
- **THEN** reviews can load normally without enabling existing analytics or altering ordering-link behavior

### Requirement: Defer and bound third-party loading
Review-specific third-party SDK and data requests SHALL start only when the enabled reviews section is within 200 CSS pixels of the viewport, or on browser initialization when viewport observation is unsupported. The section SHALL make at most one details request per page load, with no polling or automatic retries. The loading state MUST end within 10 seconds after initiation with content, an empty state, or a visible unavailable state; late responses MUST NOT overwrite a terminal timeout state. Static builds MUST NOT request review data.

#### Scenario: Open the homepage before reaching reviews
- **WHEN** the enabled section is outside the loading boundary in a browser supporting viewport observation
- **THEN** no review-specific Google SDK or details request has started and core restaurant content remains usable

#### Scenario: Repeatedly enter the loading boundary
- **WHEN** a visitor scrolls into, out of, and back into the section's loading boundary
- **THEN** the section loads the provider at most once and does not make repeated details requests

#### Scenario: Provider loading or retrieval stalls
- **WHEN** loading does not produce a terminal result within 10 seconds
- **THEN** the loading message changes to unavailable, the Google Maps link remains usable, and a late response does not replace that state

#### Scenario: Viewport observation is unsupported
- **WHEN** an enabled browser cannot observe the section's proximity to the viewport
- **THEN** the isolated enhancement makes its single bounded loading attempt on initialization

### Requirement: Present truthful review data safely
The feature SHALL show aggregate rating and total rating count only when the corresponding response fields are valid, and MUST NOT derive them from the displayed sample. Each usable review SHALL show the returned author's name nearby, individual rating when valid, available publication date, and unaltered review text when provided. Missing optional fields SHALL be omitted or explicitly described without invented values. Missing required author attribution SHALL prevent that review's display and surface a diagnostic without exposing keys or response bodies. Review text and attribution links MUST be rendered without executing provider-supplied markup or unsafe URL schemes.

#### Scenario: Show aggregate and individual data
- **WHEN** Google returns valid aggregate fields and attributed reviews
- **THEN** the summary uses Google's aggregate fields and each review shows its own returned data with readable numeric ratings

#### Scenario: Receive a rating-only review or missing optional fields
- **WHEN** an attributed review has a valid rating but no text, or lacks a publication date or profile link
- **THEN** the review is identified as rating-only where applicable, absent optional values are omitted, and no quote, date, or URL is invented

#### Scenario: Receive malformed or unsafe content
- **WHEN** a response contains markup-like review text, an unsafe profile URL, or a review without author attribution
- **THEN** text remains inert, unsafe links are not navigable, and unattributable reviews are excluded with a sanitized diagnostic; an entirely unusable nonempty response produces an unavailable state rather than a claim that no reviews exist

### Requirement: Keep provider and author attribution attached to content
Displayed Google review data SHALL include an official, unmodified Google Maps attribution asset in the same visual container and all required returned data-provider attributions. Author names SHALL appear near their reviews; available safe author-profile links SHALL be preserved. Review data MUST NOT be written to source, static build output, browser persistent storage, or an application cache. Publicly accessible terms and privacy pages SHALL incorporate Google's applicable terms/privacy references and accurately disclose third-party review loading; the footer SHALL link to both pages.

#### Scenario: Read returned review content
- **WHEN** review data is visible at desktop or mobile widths
- **THEN** Google Maps attribution, applicable provider attributions, and nearby author names remain legible and unobscured

#### Scenario: Visit policy pages without JavaScript
- **WHEN** a visitor follows the footer's privacy or terms link with JavaScript disabled
- **THEN** a static page explains the relevant Google integration and links to the applicable Google terms or privacy policy

#### Scenario: Close a page after reading reviews
- **WHEN** a review-loading page session ends
- **THEN** the application has not persisted review text, ratings, authors, or other returned content for reuse across sessions

### Requirement: Provide accessible responsive states and permanent recovery links
The reviews section SHALL have a semantic heading, a polite textual status announcement, and a permanent anchor to the supplied Google business listing in delivered HTML. It SHALL distinguish disabled, pending, loading, success, empty, and unavailable states without fabricated success data. Review content SHALL remain readable at 320 CSS pixels and wider without horizontal page overflow, with keyboard-operable links and any text-expansion controls, visible focus, and no autoplay. Full review text SHALL be accessible without additional provider requests.

#### Scenario: Disable JavaScript or block Google
- **WHEN** JavaScript is disabled or review-provider access is blocked
- **THEN** the reviews heading and business-listing anchor remain available, existing homepage actions work, and no permanent loading indicator traps the visitor

#### Scenario: Return no reviews
- **WHEN** a successful provider response includes no reviews
- **THEN** the section displays an explicit empty message, retains any valid aggregate fields with attribution, and keeps the Google Maps anchor

#### Scenario: Read on mobile or with a keyboard
- **WHEN** a visitor reads at 320 CSS pixels, zooms text, or operates the section with a keyboard
- **THEN** content and controls wrap without page overflow, full review text is reachable, focus remains visible, and loading does not steal focus

#### Scenario: Announce a loading result
- **WHEN** the section changes from pending to loading and then to a terminal state
- **THEN** its concise status is announced politely without making every review card a live region
