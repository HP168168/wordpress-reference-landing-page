# wordpress-reference-landing-page

A Codex skill that recreates a supplied webpage screenshot, mockup, or visual reference as a responsive WordPress landing page using HTML, CSS, and JavaScript.

## What it does

- Turns one or more reference images into a WordPress-ready landing page.
- Supports separate HTML/CSS/JS delivery, a Gutenberg Custom HTML block, shortcode placement, and theme/child-theme files.
- Scopes every CSS rule to a single page root so it cannot leak into the active WordPress theme.
- Isolates JavaScript in an IIFE and initializes once.
- Handles WordPress form shortcodes such as `[fluentform id="1"]`.

## Install

Copy this directory into your Codex skills folder:

```text
~/.codex/skills/wordpress-reference-landing-page/
```

Or install it through the Codex skill-installer using this repository URL.

## Usage

Use `$wordpress-reference-landing-page` to recreate a reference image as a WordPress-ready landing page.
