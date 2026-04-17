# Zelcodes — Graphic Designer Brief

A complete design-language reference for the Zelcodes brand (website, app, marketing). Hand this file to an AI (or a human designer) and ask it to produce on-brand posters, social cards, lockups, hero art, or print collateral.

The brand has **two defining visual elements** that every asset should reference:

1. **The Liquid Orbit** — a 3D glass orb with a living mesh-gradient interior and a comet orbiting on a tilted diagonal ellipse.
2. **Liquid-glass typography** — inflated, bubble-like letters filled with a continuous diagonal mesh gradient, lit from above, with a travelling specular streak.

Everything else in the brand — backgrounds, cards, buttons, type sets — exists to support those two elements.

---

## 1 · Brand positioning

- **Product**: Zelcodes — a premium library of SwiftUI / iOS animations. Developers browse animations on the web and unlock source on Patreon.
- **Audience**: working iOS and SwiftUI developers. Aesthetically-aware, design-literate.
- **Tone**: premium, modern, developer-first. Peers with Linear, Vercel, Framer, Apple developer docs.
- **Feel**: alive (something is always subtly moving), confident, glassy, a little cinematic.
- **Avoid**: skeuomorphic clutter, flat Material-style UI, neon gaming aesthetics, startup-boilerplate vibes.

---

## 2 · Color system

### 2.1 Brand palette

| Role         | Hex       | Usage                                    |
| ------------ | --------- | ---------------------------------------- |
| Indigo       | `#6366f1` | Primary brand color; gradient start      |
| Pink         | `#ec4899` | Secondary accent; gradient middle        |
| Sky          | `#38bdf8` | Tertiary accent; gradient continuation   |
| Off-white    | `#f5f1e8` | Warm off-white; gradient end, highlights |
| Patreon      | `#f96854` | Patreon CTA only                         |

The **three brand hues always appear together** as a triad. Never use indigo alone; it should always nod to the pink/sky partners somewhere in the composition.

### 2.2 Surface & text

| Role            | Light mode              | Dark mode               |
| --------------- | ----------------------- | ----------------------- |
| Background      | `#fafbff`               | `#05060f`               |
| Foreground text | `#0b0b14`               | `#f4f5ff`               |
| Muted text      | `#5b6077`               | `#9aa0b8`               |
| Glass surface   | `rgba(255,255,255,0.65)`| `rgba(20,22,40,0.55)`   |
| Glass border    | `rgba(17,17,44,0.08)`   | `rgba(255,255,255,0.08)`|

Glass surfaces use `backdrop-filter: blur(18px) saturate(140%)` + a 1px border. No solid panels — always blurred translucency.

### 2.3 The signature gradient

The **continuous diagonal brand gradient**:

```
linear-gradient(115deg,
  #6366f1 0%,       /* indigo */
  #ec4899 32%,      /* pink */
  #38bdf8 70%,      /* sky */
  #f5f1e8 100%      /* warm off-white */
)
```

Use at ~115° (top-left to bottom-right, slight vertical bias). This is the "hero" color flow of the brand. Appears on: wordmark fill, hero headlines, button backgrounds, large display type, poster headlines.

A second variant with off-white earlier in the flow, used for the wordmark to give the tail letters a pearlescent finish:

```
linear-gradient(110deg,
  #6366f1 0%, #ec4899 35%, #f5f1e8 65%, #f5f1e8 100%)
```

---

## 3 · Typography

### 3.1 Typefaces

- **Inter** — all UI, body, headings. Default weight 400; headings 600–800.
- **JetBrains Mono** — code snippets only.

### 3.2 Display type rules

- Weight **700–800** for display / wordmark / hero type.
- Letter-spacing **−0.04em to −0.055em** (tight, confident).
- Line-height **1.0** on display, **1.15** on larger headings, **1.5** on body.
- Never center-align body copy longer than two lines. Hero headlines and section titles may center.

### 3.3 Scale (rough)

- Display / hero: 56–72px
- Section title: 36–48px
- Sub-heading: 20–24px
- Body: 14–16px
- Caption / eyebrow: 11–12px, uppercase, tracked **+0.08em**

---

## 4 · The Liquid Orbit (signature mark)

### 4.1 Concept

A dark glass orb containing a **miniature version of the site's mesh gradient**: three blurred color blobs (indigo, pink, sky) orbit inside the orb at different rhythms, creating a living interior. Outside the orb, a **single photon** streaks along a **tilted, diagonal elliptical orbit** at ~−30°, with a small comet trail and depth-based opacity (brighter on the near side, dimmer when passing "behind").

Read it as: a tiny window onto the cosmos of SwiftUI animation — geometric, alive, iOS-coded, never static.

### 4.2 Construction — layers (bottom to top)

1. **Ambient halo** — three soft Gaussian-blurred circles (the brand triad) in the top-left, top-right, and bottom center of the composition. `stdDeviation: 8`, opacity 0.35–0.6 breathing.
2. **Orb well** — solid `#0b0b14` circle, radius 26 in a 72-unit viewBox.
3. **Living mesh** — three Gaussian-blurred circles (`#6366f1`, `#ec4899`, `#38bdf8`) clipped inside the orb, each animating `cx`/`cy` on 8s / 9s / 10s loops with different orbital patterns.
4. **Inner shadow** — radial gradient vignette at edge (transparent → 45% black at 100%) inside the clip. Gives the orb depth.
5. **Glass sheen** — radial gradient centered at ~30%/22%, `rgba(255,255,255,0.65)` → transparent by 70%. Top-left specular highlight.
6. **Rim** — 1.3px stroke with a diagonal gradient `rgba(255,255,255,0.9) → 0.1 → 0.6`. The rim is brighter on the top-left, fades in the middle, brightens again at bottom-right.
7. **Specular pinch** — small white ellipse at top-left, rotated −30°, 45% opacity. The "second highlight" that sells it as glass rather than plastic.
8. **Orbit ring** — a **tilted ellipse** `rx 32, ry 13, rotate(−30°)` around orb center. Dashed `2 3.5`, white at 30% opacity. Dashes flow via animated `stroke-dashoffset` (6s linear loop).
9. **Photon + trail** — a bright white `3.6r` dot wrapped in a soft `7r` halo (radial `#ffffff → #e0e7ff → #a5b4fc`). Traces the tilted ellipse. Two smaller, fainter trailing dots follow at −0.18 and −0.38 radians. Opacity and scale fade when the dot is on the "back" half (top of ellipse in screen-space).

### 4.3 Geometry constants

- Overall viewBox: `0 0 72 72`
- Orb: center (36, 36), radius 26
- Orbit ellipse: center (36, 36), rx 32, ry 13, rotated **−30°**
- The −30° tilt is the brand signature. Don't change the angle per design; it gives the mark its recognizable diagonal personality.

### 4.4 Favicon / small-scale variant

At 16×16 most detail disappears. For small sizes:

- Keep the dark orb with three blurred mesh blobs
- Keep the glass sheen + rim
- Keep the tilted orbit ellipse and the photon
- Drop the ambient halo, drop the specular pinch

---

## 5 · Liquid-glass wordmark ("zelcodes")

### 5.1 Concept

Inflated, bubble-like letterforms that look like they were blown from the same glass as the orb. Each letter is filled with the **continuous diagonal brand gradient** (so colour flows across the entire word, not per-letter) and topped with a **bright specular sheen** that reads the letters as 3D glass rather than flat typography. A travelling specular streak sweeps across every few seconds, making the type feel freshly lit.

### 5.2 Composition

The wordmark is `zelcodes` with the `o` **replaced by a small Liquid Orbit mark** that sits inline. The orb's size ≈ 0.95× the font size, translated `+0.08em` on Y so it rests on the baseline like a real letter.

### 5.3 Typography

- **Inter 800**, `font-size 22–42px` for navbar / footer / poster display
- **Letter-spacing −0.055em**
- **Line-height 1.0**

### 5.4 Glass effect (layered, all clipped to text)

Applied on the outer lockup span:

1. **Static top sheen** (layer 1):
   ```
   linear-gradient(180deg,
     rgba(255,255,255,0.55) 0%,
     rgba(255,255,255,0.15) 30%,
     rgba(255,255,255,0)    60%)
   ```
2. **Continuous diagonal colour** (layer 2):
   ```
   linear-gradient(115deg,
     #6366f1 0%, #ec4899 32%,
     #38bdf8 70%, #f5f1e8 100%)
   ```
   at `background-size: 220% 100%`. Animated left-right over 8s to create a flowing shimmer.

Both layers are `-webkit-background-clip: text; color: transparent;` so the gradient paints only within the glyph shapes.

### 5.5 Glow (drop-shadow stack)

```
filter:
  drop-shadow(0 2px 3px rgba(0,0,0,0.18))
  drop-shadow(0 0 18px rgba(129,140,248,0.38));
```

First shadow grounds the letters on the surface; second halo echoes the orb's ambient glow.

---

## 6 · Mesh-gradient background (hero / marketing)

The primary page background in hero / marketing contexts.

### 6.1 Recipe

Three oversized, heavily-blurred circles on a neutral background:

```
• Indigo blob  — top-left,  size 60vh, blur 120px, opacity 0.55
• Pink blob    — top-right, size 55vh, blur 140px, opacity 0.45
• Sky blob     — bottom-center, size 65vh, blur 140px, opacity 0.45
```

Each blob drifts on a different timeline (18s, 22s, 26s) with subtle translate + scale. Over that, a vertical linear gradient fade into the page background keeps the foot of the section clean.

### 6.2 Bold variant

For hero above-the-fold: opacity 0.85 on all blobs. For section backgrounds: opacity 0.55.

---

## 7 · Surfaces (glassmorphism)

All cards, panels, chips, pills, modals.

```
background:        var(--glass-surface);   /* translucent white or near-black */
border:            1px solid var(--glass-border);
backdrop-filter:   blur(18px) saturate(140%);
border-radius:     16–24px (cards), 9999px (pills)
```

Do not use solid-colored cards. If a surface needs to be solid (e.g. to avoid mesh bleed-through), use `background: var(--background)` with a 1px `var(--glass-border)` and a soft shadow `0 30px 70px -28px rgba(17,17,44,0.35)`.

---

## 8 · Motion & animation language

### 8.1 Easing (use these, never linear unless you mean it)

- **Brand ease**: `cubic-bezier(0.22, 1, 0.36, 1)` — the "hero reveal" easing. Primary for entrances, micro-interactions.
- **Spring**: Framer Motion `type: "spring", stiffness: 240–320, damping: 18–28`. For buttons, cards on hover.
- **Ease-in-out**: `easeInOut` — ambient loops (meshes, blobs, gradient flow).
- **Linear**: only for infinite rotations (orbit rings, halos).

### 8.2 Recurring motion patterns

| Pattern            | Duration  | Usage                                    |
| ------------------ | --------- | ---------------------------------------- |
| Breathing          | 3–5s      | Halos, pulses, subtle scale/opacity      |
| Mesh drift         | 8–10s     | Color blobs inside orb / in backgrounds  |
| Orbit revolution   | 4–6s      | Photons, dashed rings                    |
| Gradient flow      | 7–8s      | Wordmark shimmer, liquid text            |
| Specular sweep     | 5s        | Moving highlight on glass type           |
| Card entrance      | 0.4–0.6s  | `y: 16 → 0` + opacity + brand ease       |

### 8.3 Reduced motion

**Always respect `prefers-reduced-motion`**. Collapse infinite animations to static; entrance animations become instant. In code: `useReducedMotion()` → branch animations.

### 8.4 Depth cues

Motion is the primary depth cue. Static posters communicate depth via:

- Drop-shadow layering (crisp dark + soft colored glow)
- Blurred back-layers at reduced opacity
- Rotated / offset back layers peeking from behind the hero element
- Specular highlights on the top-left of round shapes

---

## 9 · Component patterns

### 9.1 Primary button (foreground-filled)

```
background: var(--foreground);
color:      var(--background);
padding:    12–14px 24–28px;
border-radius: 9999px;
font-weight: 500;
font-size: 14px;
hover: opacity 0.9; arrow icon translates +2px
```

### 9.2 Secondary button (glass)

```
glass (backdrop blur + translucent bg + 1px border);
border-radius: 9999px;
same padding / font as primary;
hover: border accent
```

### 9.3 Patreon CTA

```
background: #f96854;
color: white;
box-shadow: 0 10px 28px -8px rgba(249,104,84,0.35);
border-radius: 9999px;
icon: small heart
```

### 9.4 Eyebrow / badge

```
glass pill, 11–12px font, uppercase, tracked +0.08em,
optional leading dot in brand color
```

### 9.5 Card (animation showcase)

```
glass surface, border-radius 24px,
rounded preview image inset 8px,
title 14px / 600,
description 14px / 400 / muted,
tag row (11px pills, 1px border)
```

---

## 10 · Layout principles

- **Max width 6xl (1152px)** for content containers. Breathe.
- **Consistent padding**: 16px mobile, 24px tablet, 24px desktop, with sections at 64–96px vertical.
- **Grids**: 12-col desktop, 2–3 col for card grids.
- **Radii**: 16px (small cards), 20–24px (large cards), 32px (hero surfaces), 9999px (pills).
- **Borders**: 1px at 8% opacity on surfaces. Never solid grey lines.
- **Shadows**: colored glow (brand or brand-tinted) preferred over neutral black shadows.

---

## 11 · Applying this to poster design

When generating a poster / social card / print piece, compose from these brand ingredients:

### 11.1 Must-haves (every poster)

- One or more appearances of the **brand triad** (indigo + pink + sky). Off-white may appear as a highlight.
- The **Liquid Orbit mark** somewhere on the canvas — hero element, accent, or watermark. Its size telegraphs hierarchy.
- Type set in **Inter 700–800**, tight tracking, with at least one element using the **continuous diagonal gradient** as a fill.
- A hint of motion — either actual motion (GIF / Lottie) or implied (trailing dots, ghost-layers, drop-shadow blur, streak).

### 11.2 Default composition

- Dark or neutral mesh-gradient background (three soft brand blobs, heavy blur).
- Hero element: the Liquid Orbit at large scale, off-center, with its tilted orbit ring prominent.
- Display type in liquid-glass style (continuous diagonal gradient + bright top sheen).
- Supporting copy in muted foreground, short lines.
- Sparse use of glass cards/pills if the poster carries secondary info (date, URL, CTA).

### 11.3 Ingredient menu

- **Orb variants**: single large orb, orb trio (three in a row with rotational keyframe offsets), orb with Saturn-style rings (multiple stacked ellipses), orb-burst (photon trail broken into particles).
- **Background variants**: mesh gradient (standard), deep space (`#05060f` + distant brand blobs + noise), frosted glass panel over a saturated brand tile.
- **Type variants**: liquid-glass fill (default), outlined-glass (1px white stroke, transparent fill), chromatic-ghost (three offset text copies in the three brand hues blending via screen-mode).
- **Accents**: dashed orbit rings, drifting particles, concentric rounded rectangles (echo of the BPConcentricRectangle project), easing-curve swooshes with anchor + comet endpoints.

### 11.4 Don'ts

- Don't use the brand colors as flat fills. They should always appear in gradient, blurred blob, or glass-layer contexts.
- Don't use solid rectangles or hard edges for primary shapes. Prefer squircles, circles, blobs.
- Don't use heavy drop shadows in neutral black. Colored glows only.
- Don't use more than **one** mesh gradient "weight" per composition — mesh is the hero surface, not wallpaper-texture.
- Don't let typography compete with the orb. The orb is the focal point; type supports.

### 11.5 Quick poster recipe (for AI prompting)

> *"Dark navy-to-black background with three large blurred brand-color glows (indigo top-left, pink top-right, sky bottom). Center-left: a Liquid Orbit mark (dark glass orb with living mesh gradient inside, tilted diagonal elliptical orbit ring and a glowing white comet on the orbit at 30° angle). Right side: a two-line headline in Inter 800, 64px, tight tracking, filled with a 115° gradient from indigo → pink → sky → warm off-white, bright white specular highlight along the top of each letter. Subtle colored drop-shadow glow on the type. Thin glass pill with 11px uppercase eyebrow text at the top. Footer: one line in muted foreground."*

---

## 12 · Technical crib sheet

- **Tech stack**: Next.js (App Router) + Tailwind CSS 4 + Framer Motion + next-themes.
- **Fonts**: `next/font/google` Inter + JetBrains Mono.
- **Animated logo**: `src/components/AnimatedLogo.tsx` (Framer Motion + SMIL concepts).
- **Wordmark lockup**: `src/components/Logotype.tsx`.
- **Mesh**: `src/components/MeshGradient.tsx`.
- **Tokens**: `src/app/globals.css` (CSS custom properties + Tailwind `@theme` block).
- **Favicon**: `src/app/icon.svg` (SMIL-animated miniature orb).

Study those files when porting the aesthetic to a new medium. Every ingredient listed here has a concrete implementation in that code.
