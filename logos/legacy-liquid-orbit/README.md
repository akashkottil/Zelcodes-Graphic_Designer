# Zelcodes — Logo Asset Pack

Brand lockup: **"zelcodes"** where the `o` is replaced by the Liquid-Orbit mark. Every logo ships as **both an SVG** (fully editable, scales losslessly) **and a pre-rendered PNG** (type already rasterised with Inter 800 — drop-and-go for anywhere SVG isn't supported).

- **SVG** → Figma / Illustrator / Keynote / web
- **PNG** → Slack / Notion / Pages / decks / anywhere without SVG support
- **GIF** (animated folder only) → chat attachments, social, email signatures

All SVGs use `font-family: Inter, -apple-system, system-ui, sans-serif`. For pixel-perfect typography when opening the **SVG** files, make sure **Inter 800** is installed locally (free at [rsms.me/inter](https://rsms.me/inter/)). The PNGs are already rendered with Inter embedded, so you never need to install a font to use them.

---

## `animated/`

SMIL-animated SVGs. Open in any modern browser and they animate without any JS: mesh blobs drift inside the orb, the photon traces the tilted diagonal orbit, orbit dashes flow. Chrome / Edge / Safari animate fully; Firefox shows the first frame as a static snapshot.

| File                  | Use                                            |
| --------------------- | ---------------------------------------------- |
| `logo-animated.svg`   | Full `zelc{orb}des` lockup, transparent bg     |
| `mark-animated.svg`   | Orb only (140×140), transparent bg             |

Both are ideal for: web embeds, slide-deck hero shots, looping social video intros (export to MP4 via `puppeteer` or a browser screen-capture).

---

## `static-transparent/`

Non-animated, transparent background. The orb renders from the same paint recipe as the live logo (one fixed photon position at ~110° on the orbit). Every file is available as both `.svg` and `.png` (PNGs rendered at **1600×400** for lockups and **560×560** for the mark, transparent).

| File                      | Gradient                                                   | Use                                                                          |
| ------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `logo-gradient`           | Full 4-stop: indigo → pink → sky → off-white               | The canonical brand lockup. Default choice.                                  |
| `logo-gradient-vibrant`   | 3-stop: indigo → pink → sky (no off-white tail)            | Saturated variant for tighter compositions where you want every letter rich. |
| `logo-gradient-warm`      | Indigo → pink → warm off-white (no sky)                    | Softer, more editorial feel. Good on neutral paper.                          |
| `logo-mono-dark`          | Solid `#0b0b14`                                            | Light backgrounds, print, one-colour contexts.                               |
| `logo-mono-light`         | Solid `#f4f5ff`                                            | Dark backgrounds, print reverse, one-colour contexts.                        |
| `mark-only`               | Brand mesh (full colour)                                   | Orb alone (140×140). Favicons, app icons, stickers, watermarks.              |

---

## `with-background/`

Preset compositions at 800×400 (PNGs rendered at **1600×800**) — drop straight into a slide or social post. Each comes as both `.svg` and `.png`.

| File              | Background                                            |
| ----------------- | ----------------------------------------------------- |
| `logo-on-dark`    | Deep navy `#05060f` with three brand-colour glows     |
| `logo-on-light`   | Warm off-white `#fafbff` with three soft brand glows  |
| `logo-on-brand`   | Saturated indigo → pink → sky brand gradient field    |

All three use the 4-stop brand gradient on the type except `logo-on-brand`, which reverses to solid warm off-white (`#f5f1e8`) for contrast against the vibrant backdrop.

---

## Gradient recipes

All gradients are `linearGradient` at roughly 115° (top-left → bottom-right) over the full lockup width, so the colour flows continuously from the leading `z` through the orb to the trailing `s`.

| Variant      | Stops                                                                  |
| ------------ | ---------------------------------------------------------------------- |
| Full         | `#6366f1 0%` · `#ec4899 32%` · `#38bdf8 70%` · `#f5f1e8 100%`          |
| Vibrant      | `#6366f1 0%` · `#ec4899 50%` · `#38bdf8 100%`                          |
| Warm         | `#6366f1 0%` · `#ec4899 40%` · `#f5f1e8 100%`                          |

---

## Exporting to PNG / PDF / favicon

Open any SVG in a browser and "Save As" to get raster exports, or run:

```bash
# PNG @ 4x
rsvg-convert -z 4 logo-gradient.svg -o logo-gradient@4x.png

# PDF (preserves vectors)
rsvg-convert -f pdf logo-gradient.svg -o logo-gradient.pdf

# Favicon (32×32 from mark-only)
rsvg-convert -h 32 -w 32 mark-only.svg -o favicon-32.png
```

(install `rsvg-convert` via `brew install librsvg` if needed.)

---

## Editing tips

- Open any SVG in a text editor — the file is heavily commented via ids (`text`, `oc`, `ob`, `orim`, `op`, etc.) so you can retune.
- The **photon angle** is controlled by `rotate(110)` in the innermost `<g>` of the photon — change to move the dot around the tilted orbit (0° is the top of the un-tilted ellipse; try 30°, 150°, 220°).
- The **orbit tilt** is controlled by `rotate(-30)` on the photon group AND the `<ellipse>` transform — keep them matched.
- The **text gradient** uses `gradientUnits="userSpaceOnUse"` so it spans the whole viewBox — move stops or change hex to explore colour fades.

---

## License

These assets are the visual identity of Zelcodes by Akash Kottil. Reuse is fine for anything related to the Zelcodes project (documentation, ports, articles, press). Everywhere else: ask first.
