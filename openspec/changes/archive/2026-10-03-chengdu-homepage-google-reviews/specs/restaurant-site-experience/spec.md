## MODIFIED Requirements

### Requirement: Preserve the restaurant home presentation
The site SHALL retain the home page's restaurant identity, responsive video hero, delivery/pickup/menu actions, featured dishes, restaurant features, gallery, about text, location section, and footer. Existing red/gold styling, fonts, dish images, image descriptions, and AI image labels MUST remain recognizable at desktop and mobile sizes. A Google reviews section SHALL appear after dining options and before About, without changing the relative order of existing sections; its content and fallback behavior SHALL follow the `google-review-display` capability.

#### Scenario: Browse the home page on desktop or mobile
- **WHEN** a visitor opens `/` at a desktop or mobile viewport
- **THEN** the existing sections, copy, media, and ordering actions are presented in their established relative order, with the added reviews section after dining options and before About, without clipped controls or horizontal page overflow

#### Scenario: Video playback is unavailable
- **WHEN** a browser cannot autoplay or load the background video
- **THEN** the restaurant title, hero layout, and action links remain visible and usable

#### Scenario: Google reviews are unavailable
- **WHEN** review configuration is disabled or Google review retrieval fails
- **THEN** the Google Maps fallback link is available and existing homepage content, ordering destinations, and location access remain unchanged
