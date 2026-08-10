# The Nightingale Society — Style Guide

## Color Palette
Sampled from the club logo (purple background, illustrated nightingale on a branch).

| Name | Hex | Use |
|---|---|---|
| Plum (primary) | `#3E2A45` | Page/section backgrounds, header |
| Parchment (light) | `#EDE0C8` | Text on dark backgrounds, card backgrounds, borders |
| Gold (accent) | `#CB9C6E` | Buttons, links, highlights, active states |
| Sand (secondary accent) | `#D8C0A0` | Tags, dividers, subtle backgrounds |
| Deep Brown (neutral) | `#2A1E18` | Body text on light backgrounds |

CSS variables used across every page:

```css
:root {
  --ns-plum: #3E2A45;
  --ns-parchment: #EDE0C8;
  --ns-rust: #CB9C6E;
  --ns-sand: #D8C0A0;
  --ns-brown: #2A1E18;
}
```

## Typography
- **Headings**: [Playfair Display](https://fonts.google.com/specimen/Playfair+Display) — elegant serif matching the logo's vintage badge lettering.
- **Body**: [Lora](https://fonts.google.com/specimen/Lora) — readable serif that pairs well with Playfair Display.
Loaded on every page via:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600;700&family=Lora:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
```

## Logo
File: `assets/nightingale-logo-transparent.png` — background removed, cropped tight to the circular badge (transparent corners).
- In the Home hero, it sits in the open space to the right of the headline, centered between the end of the text and the hero's right edge (see `index.html`'s `hero__logo-slot`). It also appears in the nav bar brand mark on every page.
- The gold accent color (`#CB9C6E`) is a warm tan drawn from the logo's tones, so buttons/links stay in the same family as the artwork.

## Motif
The hero uses the logo badge itself as the bird illustration, plus periodic **chains of toon-shaded books** (cover + a lighter "pages" edge), colored from the site palette, that swoop across the top, loop, trail sparkles, and fade out on repeat — literary and a little playful, without relying on a second illustration style.
