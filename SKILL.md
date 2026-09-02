---
name: wordpress-reference-landing-page
description: Recreate a supplied webpage screenshot, mockup, or visual reference as a responsive WordPress landing page using HTML, CSS, and JavaScript. Use when the user wants to turn a reference image into a WordPress-ready page, optionally generate new image assets or use client-supplied assets, isolate all styles from the active WordPress theme, embed WordPress shortcodes or form placeholders, and deliver code for separate HTML, CSS, and JavaScript fields or a Custom HTML block.
---

# Build a WordPress Landing Page from a Reference

Create a visually faithful, responsive landing page from one or more reference images. Treat the reference as design direction, not as permission to copy protected brand assets or proprietary text verbatim.

## Establish the delivery format

Before coding, identify the WordPress integration surface from the user's screenshot or description:

- Separate HTML, CSS, and JavaScript tabs: deliver three paste-ready files or code blocks.
- Gutenberg Custom HTML block: deliver a fragment without `doctype`, `html`, `head`, or `body`. Warn that WordPress may strip scripts and may not execute shortcodes inside this block.
- Shortcode block: place forms such as `[fluentform id="1"]` here when the HTML block prints the shortcode as text.
- Theme, child theme, or template file: provide the appropriate PHP/HTML structure only when explicitly requested.

Never give a complete standalone HTML document when the destination accepts only an HTML fragment.

## Inspect before building

1. View the reference at its original resolution.
2. Inventory every visible section, image, repeated component, heading level, CTA, form, navigation item, background change, and responsive concern.
3. Identify the page's visual system:
   - content width and outer gutters;
   - typography roles and scale;
   - brand and neutral colors;
   - spacing rhythm;
   - image aspect ratios and focal points;
   - borders, corners, shadows, and motion.
4. Use the user's real copy, brand facts, colors, logo, image URLs, and shortcode values. Do not invent certifications, clients, testimonials, factory statistics, contact details, or guarantees.
5. Note repeated sections and remove them when they add no new conversion or information value.

## Choose the image workflow

### Generate new images

Use the image-generation skill when original photography or product imagery is required.

- Create one file per distinct asset; do not generate a screenshot collage and crop it into assets.
- Match the intended display ratio in the generation prompt: hero, card, banner, portrait, or mosaic.
- Give each asset a descriptive lowercase SEO filename such as `custom-eyewear-manufacturer-hero.webp`.
- Require no watermark, no accidental text, no invented logos, and physically plausible products, hands, machinery, or architecture.
- Inspect every generated image before embedding it. Regenerate malformed products, hands, faces, text, or manufacturing actions.
- If the user converts assets to WebP, update every direct source and every JavaScript-driven image path, not just `<img>` elements.

### Use client images

- Preserve the supplied filenames unless SEO renaming is requested.
- Ask for or infer the public WordPress upload base URL.
- Prefer same-origin root-relative paths such as `/wp-content/uploads/2026/08/` to avoid HTTP/HTTPS mixed-content problems.
- Keep the base path in one JavaScript constant when many images share a directory.
- Use meaningful `alt` text describing the image's purpose; do not keyword-stuff.

## Build the page

### HTML rules

- Wrap the entire fragment in one unique root, for example:

```html
<div class="brand-landing-page">
  <!-- page sections -->
</div>
```

- Use semantic sections, headings, navigation, lists, figures, buttons, and accessible labels.
- Use real `<button>` elements for interactive controls and anchors for navigation.
- Keep heading order logical.
- Add `loading="lazy"` to non-hero images and explicit intrinsic width and height when known.
- Put the WordPress form shortcode at the intended form position, but explain the fallback Shortcode-block requirement.
- Omit the site-wide footer or header when the user's WordPress theme already supplies it, unless the reference or user explicitly requires a page-local version.

### CSS isolation rules

Scope every rule to the unique page root so the landing page cannot modify the theme or other pages.

Good:

```css
.brand-landing-page { --brand: #0f2154; }
.brand-landing-page,
.brand-landing-page * { box-sizing: border-box; }
.brand-landing-page h2 { color: #10131a !important; }
.brand-landing-page .dark-section h2 { color: #fff !important; }
```

Avoid unscoped selectors such as:

```css
body {}
h2 {}
img {}
button {}
details {}
```

Use `.brand-landing-page h2`, `.brand-landing-page img`, and equivalent scoped selectors instead.

Additional safeguards:

- Do not reset `html`, `body`, `:root`, or every element globally.
- Store design tokens on the page root, not `:root`.
- Use `!important` only for high-risk theme conflicts such as heading colors, link states, button text colors, form controls, or builder-imposed widths.
- Define normal, `:visited`, `:hover`, `:focus`, and `:active` colors for CTA links because themes frequently override them.
- If the page must escape a Gutenberg content column, use a root-level full-width rule deliberately:

```css
.brand-landing-page {
  width: 100vw;
  max-width: none;
  margin-left: calc(50% - 50vw);
  margin-right: calc(50% - 50vw);
  overflow: hidden;
}
```

- Respect `prefers-reduced-motion` and include visible keyboard focus.

### Image sizing rules

Prevent intrinsic HTML dimensions from stretching images:

```css
.brand-landing-page img {
  display: block;
  max-width: 100%;
  height: auto;
}
```

Then override only intentional crop containers:

```css
.brand-landing-page .hero img,
.brand-landing-page .media-cover img {
  width: 100%;
  height: 100% !important;
  object-fit: cover;
}
```

Use `object-fit: contain` for white-background catalog products when the complete frame must remain visible. Use `cover` for editorial photography. Set `object-position` per asset when the focal point is off-center.

Never rely on `aspect-ratio` alone while an HTML `height` attribute remains effective. Verify the computed display dimensions.

### JavaScript isolation rules

- Wrap code in an IIFE.
- Query inside the page root only.
- Initialize once using a data flag.
- Do not attach broad handlers to all links, buttons, forms, or details on the WordPress page.
- Keep the upload base URL in one constant.
- Avoid dependencies unless the existing WordPress environment explicitly provides them.
- Remove demo form-submission handlers when a real WordPress form plugin replaces the mock form.

## WordPress form handling

For Fluent Forms, place the requested shortcode exactly, for example:

```text
[fluentform id="1"]
```

Scope optional styling through the page root and Fluent Forms classes. Do not reproduce the plugin's full form markup manually. If the page builder's HTML field does not execute shortcodes, instruct the user to place a Fluent Forms widget or Shortcode block at that location.

## Validate visually

Do not stop at checking whether files exist.

1. Preview the page in a browser or the user's WordPress preview when available.
2. Inspect at least one desktop width around 1440 px and one mobile width around 390 px.
3. Check every image's natural dimensions, computed display dimensions, `object-fit`, and `object-position`.
4. Look specifically for:
   - stretched cards caused by width/height attributes;
   - black or white gaps below cover images;
   - navigation or grid rows leaving empty space;
   - headings with orphaned one-letter words;
   - theme-overridden heading and button colors;
   - horizontal overflow;
   - duplicate product sections;
   - malformed generated products or hands;
   - shortcodes displayed as plain text.
5. Test menus, tabs, accordions, anchor links, and form placement.
6. After every CSS or asset correction, reload and inspect the affected section again.

## Deliver the result

Provide the artifacts in the exact fields the user has:

- `html.txt`: page fragment only.
- `css.txt`: fully page-scoped styles only.
- `javascript.txt`: isolated interaction code only.
- Image folder or final public URL mapping when assets are part of the task.

State which field changed during revisions so the user only needs to replace the necessary tab. Mention any remaining WordPress-specific action, such as uploading images or moving a shortcode into a Shortcode block.
