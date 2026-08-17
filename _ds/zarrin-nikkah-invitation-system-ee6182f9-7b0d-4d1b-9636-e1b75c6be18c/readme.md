# Zarrin — Nikkah Invitation Design System

**Zarrin** (Urdu/Persian for *golden*) is a design system for building luxe, mobile-first
Muslim / Pakistani **Nikkah & wedding invitations** as scrolling web cards. It captures the
ivory-and-champagne-gold aesthetic of high-end animated invitation reels: Mughal ogee arches,
fine gold linework, flourished calligraphy, gold-foil reveal cards, an ornamented event
timeline, a live countdown, and a pastel dress-code palette.

Everything is tuned to render **razor-crisp on every phone and tablet aspect ratio** — the
ornaments are vector (SVG), type is fluid (`clamp()`), and the invitation lives in a fixed
480px column that centres as a card on wider screens. Nothing rasterises or blurs across DPRs.

## Sources
- **`Design_culture_frames/`** — 14 frames (1080×1920) from a social-media invitation reel
  (watermark: *webgency_invitations*). These were the sole visual reference; palette, motifs,
  layout, typography, and copy were extracted from them. Working copies live in `frames/`.
- A user-supplied reference HTML (a self-contained "Nikkah Invitation" prototype) informed the
  interaction model (envelope gate, reveal cards, countdown, scroll reveals) and confirmed a
  Pinyon Script / Cormorant Garamond / Jost type stack.
- No brand logo was provided. There is **no real logo**; the wordmark "Zarrin" is set in the
  script face (`assets/logo-wordmark.svg`) purely as a system identity, not a client brand.

## CONTENT FUNDAMENTALS
- **Voice:** warm, reverent, celebratory. Second person to the guest ("You are invited…",
  "Will you join us"), first-person-plural for the couple ("as we begin our forever").
- **Casing:** section titles in flourished **Title Case script** ("The Date", "Wedding Timeline",
  "The Celebration Begins"). Structural labels in **letter-spaced UPPERCASE** serif/sans
  ("YOU ARE INVITED TO THE NIKKAH CEREMONY OF", "DAY · MONTH · YEAR", "SON OF").
- **Faith framing:** opens with the Bismillah (﷽ / بسم الله الرحمن الرحيم); includes Islamic
  events (Salat al Isha, Rukhsati) and a closing dua ("May Allah bless this union…").
- **Register:** formal but tender — "request the honour of your presence", "an evening of love,
  laughter, duas and unforgettable memories".
- **Emoji:** never. Ornamentation is carried by gold vector motifs, not emoji or unicode icons.
- **Numerals:** dates spelled long ("10 · January · 2027"); countdown uses tabular figures.

## VISUAL FOUNDATIONS
- **Colour:** warm **ivory paper** (`--paper-1` #FAF5EC) as the near-universal background;
  **champagne→antique gold** (`--gold-400` #C9A45E primary, `--gold-600` #9A7734 for gold text)
  as the single accent; **warm taupe-brown ink** (`--ink-500` #7C6A57) for body — never a cool
  neutral grey. A soft pastel set (lilac/peach/butter/blush/powder/stone) appears only in the
  dress-code section. At most one background tone per screen.
- **Type:** three voices — *Pinyon Script* (flourished calligraphy: section titles & names),
  *Cormorant Garamond* (invitation serif & letter-spaced all-caps), *Jost* (small
  letter-spaced sans labels & buttons). Fluid ramp via `clamp()` so text never drops below
  legible size on any device.
- **Backgrounds:** flat ivory with a barely-there dotted paper grain (`--grain`); a gentle
  top-down vignette on hero sections (`--grad-page`). No photographic full-bleed backgrounds;
  imagery sits inside arch-clipped or framed slots.
- **Ornament:** all decoration is **thin gold vector linework** — Mughal ogee arches
  (`non-scaling-stroke` so the outline never thickens), corner floral sprays, diamond &
  flourish dividers, a rosette timeline node, a wax seal, and five timeline medallions
  (arch, lantern, bride, dome, dhol). Crisp at any scale.
- **Motion:** slow and silky (`--ease-silk`, `--dur-med` .75s). Envelope flap opens on 3D
  rotateX; foil cards flip on rotateY; sections fade-and-rise on scroll (IntersectionObserver);
  a Ken-Burns-free, restrained feel. All motion collapses under `prefers-reduced-motion`.
- **Elevation:** warm brown-tinted shadows only (`--shadow-card`, `--shadow-lift`), plus an
  embossed inset (`--inset-emboss`) for the letterpress-arch feel. The invitation column has a
  broad soft halo (`--shadow-col`).
- **Corners:** soft jewellery-box radii — cards `--r-md` (14px), buttons pill (`--r-pill`).
- **Foil:** gold-foil surfaces use `--grad-foil` (a 135° champagne→antique gradient) with a
  diagonal white sheen and an inset hairline frame — used on the date reveal-card fronts.
- **Borders:** hairline gold (`color-mix` of `--gold-400` at 40–55% alpha), never solid black.
- **Layout:** a single centred column (`--col-width` 480px); generous fluid vertical rhythm
  (`--section-y`); everything centre-aligned; hit targets ≥ 44px.

## ICONOGRAPHY
- No icon font and no third-party icon set. All "icons" are **bespoke gold vector ornaments**
  in `assets/*.svg`, also available inline (and mirror-flippable) via the `Ornament` component:
  `corner-spray`, `seal`, `node`, `arch`, `lantern`, `bride`, `dome`, `dhol`, plus dividers.
- The inline `Ornament` versions are token-coloured (`var(--gold-*)`) so they inherit the
  palette and never collide on gradient ids; the `.svg` files are self-coloured for `<img>` use.
- Emoji and unicode dingbats are not used. The only non-Latin glyph is the Bismillah, set in the
  serif face as text.

## Components
Reusable primitives (namespace `window.ZarrinNikkahInvitationSystem_ee6182`):
- **Button** *(core)* — gold call-to-action; `outline` / `solid` (foil) / `ghost`; sizes.
- **Divider** *(core)* — gold rule; `diamond` / `flourish`.
- **SectionHeading** *(core)* — eyebrow + script/serif title + divider.
- **ArchFrame** *(decor)* — cusped Mughal ogee arch panel wrapping any content.
- **Ornament** *(decor)* — inline gold motif by name, mirror-flippable.
- **SwatchRow** *(decor)* — embossed colour circles (dress-code shades).
- **RevealCard** *(invitation)* — gold-foil card that flips to reveal a date part.
- **Timeline** *(invitation)* — vertical gold spine with alternating ornamented entries.
- **Countdown** *(invitation)* — live Days/Hours/Minutes/Seconds in Garamond numerals.

## UI Kits
- **`ui_kits/invitation/index.html`** — the complete, self-contained flagship: tap-to-open
  envelope gate → arch hero → date reveal → arch invitation panel → timeline → countdown →
  location (photo + map) → dress code → RSVP → dua footer. Uses `<image-slot>` for the couple
  photo, venue photo, and dress-code illustration (drag-and-drop fillable). Renders standalone
  with no build step.

## Templates
- **`templates/nikkah-invitation/NikkahInvitation.dc.html`** — the design-system-native, fully
  editable version, composed from the components above. Copy this folder to start a new
  invitation; edit text in place and swap component props.

## Index / manifest
- `styles.css` — global entry (import list only). Consumers link this one file.
- `tokens/` — `colors.css`, `typography.css`, `spacing.css`, `effects.css`, `fonts.css`, `base.css`.
- `assets/` — gold vector ornaments, timeline icons, seal, wordmark.
- `components/{core,decor,invitation}/` — primitives (`.jsx` + `.d.ts` + `.prompt.md` + card).
- `guidelines/` — foundation specimen cards (Colors, Type, Spacing, Effects, Brand).
- `ui_kits/invitation/` — flagship screen.
- `templates/nikkah-invitation/` — copyable DC template.
- `thumbnail.html` — homepage tile. `SKILL.md` — Agent-Skills wrapper.

## CAVEATS — please help me get these perfect
- **Fonts are Google Fonts approximations.** The reel's exact calligraphy is unknown; I used
  **Pinyon Script**, **Cormorant Garamond**, and **Jost**, loaded via `@import` in
  `tokens/fonts.css` (so the compiler reports "0 font-face" — they still load at runtime for
  consumers). If you have the original font files, drop them in and I'll wire real `@font-face`.
- **Ornaments are original vector interpretations**, not vectorisations of the reel's raster
  florals. They match the *style* (fine gold linework) and stay crisp everywhere, but the ornate
  photoreal peonies/medallions from the video can't be reproduced pixel-for-pixel from frames.
  Provide transparent PNG/SVG florals and I'll swap them into the corners and timeline.
- **Images are empty `<image-slot>`s** (couple photo, venue photo, dress-code illustration).
  Drag your real photos in, or send them and I'll embed.
- **Placeholder details** — names (Daanish & Adeena), families, Dubai/Four Seasons venue, date
  2027-01-10, and the WhatsApp number are all sample copy pulled from the reel. Send the real
  details and I'll set them across the kit and template.
