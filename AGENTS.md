<!-- bmad:context -->
<!-- Verified 2026-08-31 against 59ca093. Managed by bmad-project-context; edits inside this block are replaced on refresh. Keep anything you want preserved outside the markers. -->

## pequeno-hermeneuta-landing

Landing page for "O Pequeno Hermeneuta", a publishing imprint dedicated to children's books translating philosophy and spirituality. Stack uses vanilla HTML5, CSS3, and JavaScript. Planning lives in `_bmad-output/` and code execution rules here.

## Policy

- Always build mobile-first; write base CSS for mobile viewports, overriding for larger screens.
- Keep the branding and content focused on the "O Pequeno Hermeneuta" imprint as a whole, positioning "Saudade de Ti" as the premier book, not the sole focus of the landing page.

## Where things are

- HTML markup: `index.html`
- Styling and layout: `style.css`
- Static images and book media: `assets/`

## Running and verifying

- Verify layout changes across mobile, tablet, and desktop viewports during development.
- Serve the landing page locally using `python3 -m http.server` for testing.

## Conventions that differ from defaults

- Define base styles for mobile screens first; use `@media (min-width: ...)` queries for layout enhancements on larger screens.

## Known pitfalls

- Avoid labeling the page exclusively as "Saudade de Ti" — it represents the entire publishing imprint.

<!-- /bmad:context -->
