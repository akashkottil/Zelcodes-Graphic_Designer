# Zelcodes — Social Poster #1

Your first Zelcodes social post. Hook: **"Where SwiftUI devs orbit now."** — leans into the Liquid-Orbit metaphor that anchors the brand.

## Files

| File           | What it is                                                                 |
| -------------- | -------------------------------------------------------------------------- |
| `poster.png`   | 2160×2160 render at 2× for Instagram / X / LinkedIn square posts           |
| `poster.svg`   | **Editable source** — drop into Figma or any vector editor to modify       |
| `README.md`    | This file                                                                  |

## Specs

- **Canvas**: 1080 × 1080 (standard Instagram/X square), rendered @ 2× for retina
- **Typography**: Inter 800 (headline) / 500 (subhead) / 700 eyebrow — embedded at render time via Google Fonts
- **Palette**: Full brand triad (indigo `#6366f1`, pink `#ec4899`, sky `#38bdf8`) + off-white `#f5f1e8`
- **Background**: `#05060f` deep navy with three soft brand-colour glow blobs and a subtle dot grid

## Design ingredients (from the brand brief)

- **Big hero Liquid Orbit** (`layer-hero-orb`): dark glass well, three-blob mesh interior, glass sheen + rim + specular pinch, tilted diagonal orbit ring (−30°) with a white comet on the path
- **4 "developer" satellite orbs** on an outer tilted ellipse — indigo, pink, sky, pink-pink — glowing via `sat-glow` filter. The visual hook: devs are tiny worlds orbiting the Zelcodes star.
- **Liquid-glass headline**: `Where SwiftUI devs / orbit now.` in Inter 800 at 96pt with a 4-stop diagonal gradient fill + a top-down white sheen overlay (two stacked text elements clipped identically)
- **Eyebrow pill** top-left: `LIVE · SWIFTUI ANIMATIONS` with a pulsing sky dot (the pulse survives in the SVG when viewed in a browser; it's frozen in the PNG)
- **Footer** bottom: mini-orb + gradient wordmark on the left, `zelcodes.com →` on the right

## Editing in Figma

The SVG is structured with **labeled top-level groups** (`id="layer-background"`, `layer-eyebrow`, `layer-hero-orb`, `layer-headline`, `layer-subhead`, `layer-footer`) so Figma imports it as a clean, editable layer tree.

**To import:**
1. Open Figma, create a blank file
2. **File → Import…** and pick `poster.svg`, **or** simply drag `poster.svg` onto the canvas
3. The poster arrives as a frame with each section as a named group you can rename, recolor, reposition, or duplicate
4. Install [Inter](https://rsms.me/inter/) in Figma if it isn't already there — otherwise Figma will substitute a fallback and the type will look slightly off

**Common edits you'll probably want to make:**
- **Change the hook copy** — double-click either line of the headline text
- **Shift the satellite positions** — click any `sat-front-N` / `sat-back-N` circle and move it; they're free-floating
- **Retune gradient stops** — select the `headline-grad` paint in the properties panel and edit the colour stops
- **Swap the background** — the `layer-background` group contains the base rect + three radial-gradient rectangles; disable or recolour any
- **Resize for other socials** — duplicate the frame and resize (e.g. 1080 × 1920 for Instagram Story); regrow the orb and reflow text manually

## Re-rendering PNGs

The SVG is the source of truth. When you edit it, regenerate the PNG with **any** of:

```bash
# macOS: with librsvg installed (brew install librsvg)
rsvg-convert -w 2160 -h 2160 poster.svg -o poster.png

# Or via Chrome headless (already on your machine)
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --headless --disable-gpu --window-size=2160,2160 \
  --screenshot=poster.png \
  "file://$PWD/poster.svg"
```

## Why an SVG instead of a `.fig` file?

Figma's native `.fig` binary format is private and can't be generated from outside Figma. **But** Figma's SVG importer produces a full, editable Figma design tree from a well-labelled SVG — gradients, groups, text, and all. The SVG here is the Figma source; it just happens to also be a web-ready asset and a vector print master.

---

Brand language in full: see [`graphicdesigner.md`](https://github.com/akashkottil/Zelcodes-Graphic_Designer/blob/main/graphicdesigner.md) in the parent repo.
