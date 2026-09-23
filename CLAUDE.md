# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A folder of standalone HTML slide decks generated with the `power-design` skill, styled with a Vodafone-inspired brand system. There is no build system, package manager, linter, or test suite — each `.html` file is a fully self-contained artifact (inline CSS, base64-embedded images, vanilla JS, no external JS dependencies) that opens directly in a browser.

Current files:
- `kai-gehrke-slide.html` — single title slide (name + portrait)
- `kai-gehrke-deck.html` — multi-slide deck with animated slide transitions (title slide + "favourite club" slide)

## Working with these files

To view a deck, open the `.html` file directly in a browser (e.g. `open "kai-gehrke-deck.html"`). There is no dev server or compile step.

### Structure conventions used across decks

- Fixed **1920×1080** canvas (`.deck` / `.slide`), scaled to fit the viewport at runtime via an inline `<script>` that computes `Math.min(innerWidth/1920, innerHeight/1080)` and applies a CSS `transform: scale()`.
- Brand tokens are CSS custom properties on `:root`: `--red` (`#e60000`), `--charcoal` (`#25282b`), `--white`, `--grey`, `--light-neutral`.
- Typography is Google-hosted **Inter** (400/600/700/800), uppercase display headlines at 126px/800-weight with tightened letter-spacing, substituting for Vodafone's proprietary corporate typeface.
- Photos are embedded as `data:` URIs (base64) directly in `<img src>` — there are no separate image asset files. When adding a new photo, base64-encode it and inline it rather than referencing an external path, to keep each deck a single portable file.
- Multi-slide decks (`kai-gehrke-deck.html`) use a `.slide` / `.is-active` class toggle driven by a small IIFE at the bottom of the file: `goTo(index)` swaps the active slide, updates nav dots, and relies on CSS `transition` (opacity + `translateX`, 450ms, eased) for the animated change. `prefers-reduced-motion` disables the transform.
- Every slide keeps a 96px safe-zone inset (`.safe`) and a bottom-left brand logo mark (inline SVG circle + speech-mark path) with a small wordmark label.

### Design source

The brand styling follows `brands/vodafone/brand-style.md` and the slide rulebook in `principles/design-principles.md`, both from the `power-design` skill (`~/.claude/skills/power-design/`) — consult those if extending the brand system or adding slides, rather than inventing new tokens ad hoc.
