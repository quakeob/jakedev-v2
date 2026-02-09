---
title: "How I Made One Website Look Like Eight Different Websites"
description: "Themes aren't color swaps. Each theme on this site has its own hero layout, background animation, and visual personality."
date: 2026-02-05
tags: ["css", "design", "web-dev", "astro"]
---

# How I Made One Website Look Like Eight Different Websites

Click the theme switcher at the bottom of this page. Go ahead, I'll wait.

Notice how it's not just the colors changing? Each theme has a completely different hero section — different layout, different typography, different background animation, different *vibe*. The Terminal theme has a command prompt. The Brutalist theme has raw, aggressive type. The Paper theme looks like a newspaper masthead.

This isn't a CSS variable swap. This is eight different websites sharing one codebase.

## The Architecture

Every theme controls three layers:

1. **CSS custom properties** — colors, fonts, spacing, border-radius
2. **Hero layout** — each theme has its own HTML hero section, shown/hidden with CSS
3. **Background canvas** — each theme has a dedicated `<canvas>` element with its own animation

The trick is that all eight hero layouts exist in the DOM simultaneously. CSS controls which one is visible based on the `data-theme` attribute on `<html>`.

```css
.hero-layout { display: none; }

:root:not([data-theme]) .hero-default { display: block; }
[data-theme="terminal"] .hero-terminal { display: block; }
[data-theme="brutalist"] .hero-brutalist { display: block; }
/* ... etc */
```

Same idea for the canvas backgrounds. All eight canvases are in the DOM. Each one runs its own animation loop but only renders when visible.

## Making Each Theme Feel Authentic

The hardest part isn't the technical implementation. It's making each theme feel like a *real* design choice, not a gimmick.

### Terminal

Everything uses a monospace font. The hero is styled as shell output — `$ whoami`, `$ cat about.txt`, `$ ls projects/`. The background is a subtle matrix-style rain. The cursor blinks. It feels like SSHing into someone's server and finding their portfolio.

### Brutalist

Giant, heavy type. No rounded corners anywhere. Raw black borders. The accent color is aggressive red. The background has harsh geometric shapes. Nothing is polite about it.

### Glass

Frosted glass cards. Soft gradients. Generous border-radius. Everything feels like it's floating. The background has drifting orbs with blur effects. It's the aesthetic Apple wishes they invented (they did, but we're doing it better).

### Paper

This one's my favorite detail-wise. Georgia serif throughout. The hero looks like a newspaper masthead with decorative rules and "Est. 2026" in small italic text. The background has a subtle paper texture. It feels like a design from a different era.

## The CSS Custom Properties

Each theme defines ~20 custom properties:

```css
[data-theme="terminal"] {
  --bg: #0a0a0a;
  --text: #00ff41;
  --accent: #00ff41;
  --surface: #111;
  --border: #1a3a1a;
  --font-mono: 'JetBrains Mono', monospace;
  --radius: 0px;
  /* ... */
}
```

These cascade through everything — navigation, cards, buttons, code blocks. One attribute change propagates everywhere instantly.

## What I Learned

**Themes aren't skins.** If you just swap colors, the result feels cheap. Real theming means rethinking layout, typography, spacing, and interaction patterns for each aesthetic.

**Canvas backgrounds are expensive.** Eight animation loops in the DOM is... a lot. I optimize by only running the active canvas's animation frame loop. Inactive canvases don't requestAnimationFrame.

**CSS `display: none` is your friend.** Hidden hero layouts don't affect performance meaningfully. The browser doesn't paint them. This is way simpler than dynamically swapping components.

**Test every theme with every page.** This is the annoying part. Every new component needs to look right in eight different visual contexts. I broke the Brutalist theme at least four times while building other features.

The theme system was originally a fun experiment. It turned into the most technically interesting part of the entire site. Sometimes the side quest becomes the main quest.
