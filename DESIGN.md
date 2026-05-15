# Design System — Sreekanth Mekala Portfolio

## Product Context
- **What this is:** Personal iOS developer portfolio for Sreekanth Mekala, Senior iOS Developer at JPMorgan Chase
- **Who it's for:** Recruiters, hiring managers, and potential collaborators evaluating senior iOS engineering talent
- **Space/industry:** Personal portfolio, iOS / fintech / healthtech
- **Project type:** Single-page marketing site with cinematic scroll experience

## Memorable Thing
> "An iOS developer who treats their portfolio the way Apple treats a product launch — every detail is choreographed, nothing is accidental."

Every future design decision should serve this. If an element doesn't feel intentional, it's wrong.

## Aesthetic Direction
- **Direction:** Dark Cinematic Motion
- **Decoration level:** Intentional — marquee GIF strip and gradient headings carry all decorative weight. No blobs, no background textures, no decorative SVGs.
- **Mood:** Studio-dark with deliberate animation choreography. Feels like an iOS app built with web technology — polished, kinetic, confident.

## Typography
- **Display / Hero:** Kanit 900 — heavy, wide, self-assured. Unusual for iOS developer portfolios (which trend toward Inter/Nunito). That's the point.
- **Section headings:** Kanit 900, uppercase, `letter-spacing: -0.02em`
- **Sub-headings / card titles:** Kanit 700
- **Body:** Kanit 400 — lean at reading sizes, pairs cleanly with the heavy display cuts
- **Labels / buttons:** Kanit 500, uppercase, `letter-spacing: 0.15em`
- **Loading:** Google Fonts CDN — `https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;700;900&display=swap`
- **No fallback to system-ui / -apple-system for display** — if Kanit doesn't load the layout breaks anyway

### Type Scale (fluid via clamp)
| Role | Size |
|---|---|
| Hero / display | `clamp(5rem, 18vw, 16rem)` |
| Section heading | `clamp(3rem, 12vw, 10rem)` |
| Card title (number) | `clamp(2.5rem, 6.5vw, 90px)` |
| Card heading | `clamp(1.5rem, 3vw, 2.5rem)` |
| Sub-heading | `clamp(.9rem, 1.8vw, 1.9rem)` |
| Body | `clamp(.95rem, 1.2vw, 1.1rem)` |
| Label / button | `clamp(.7rem, .9vw, 1rem)` |
| Meta / dates | `clamp(.7rem, 1.1vw, 1rem)` |

Line-height: `1` on display, `1.5` on body. Letter-spacing: `-0.02em` on display headings, `0.15em` uppercase on buttons.

## Color

**Approach:** Restrained dark palette with a signature teal accent and a deliberately wild CTA gradient.

| Token | Value | Usage |
|---|---|---|
| `--bg` | `#0C0C0C` | Base surface, all sections |
| `--surface` | `#141414` | Card backgrounds |
| `--border` | `rgba(215,226,234,.15)` | Card borders, dividers |
| `--border-strong` | `rgba(215,226,234,.3)` | Active/hover borders |
| `--text` | `#D7E2EA` | Primary text |
| `--text-muted` | `rgba(215,226,234,.5)` | Dates, metadata, descriptions |
| `--accent` | `#4fd1c7` | Teal — links, highlights, service numbers |
| `--heading-gradient` | `linear-gradient(180deg, #646973 0%, #BBCCD7 100%)` | Hero title, section headings |
| `--cta-gradient` | `linear-gradient(123deg, #18011F 7%, #B600A8 37%, #7621B0 72%, #BE4C00 100%)` | Primary CTA button only |

**Dark mode:** This site is dark-only. No light mode.

**Color rules:**
- `--accent` is used sparingly — section numbers, skill badge borders, active states
- `--heading-gradient` is used on every major heading and never on body text
- `--cta-gradient` is used on the primary contact button only — it's a brand signature, not a pattern
- White (`#fff`) does not appear as a section background — the services section fix (2026-05-15) removed the last instance

## Spacing

- **Base unit:** 8px
- **Density:** Comfortable — generous section breathing room, tight card interiors
- **Section padding:** `clamp(4rem, 8vw, 10rem)` vertical, `clamp(1.25rem, 5vw, 2.5rem)` horizontal
- **Card padding:** `clamp(.75rem, 1.5vw, 1.75rem)`
- **Gap (grids):** `0.6rem` for image grids, `clamp(1.5rem, 3vw, 3rem)` for content gaps

### Spacing Scale
| Name | Value |
|---|---|
| 2xs | 2px |
| xs | 4px |
| sm | 8px |
| md | 16px |
| lg | 24px |
| xl | 32px |
| 2xl | 48px |
| 3xl | 64px |

## Layout

- **Approach:** Hybrid editorial — full-viewport hero + pinned sticky project cards for dramatic beats; document flow for experience and contact
- **Max content width:** `900px` for text-heavy sections, `100%` for full-bleed hero/marquee/cards
- **Grid:** Single column for mobile, document flow for desktop (no multi-column grid on text sections)
- **Border radius:** `clamp(14px,2.5vw,40px)` on image cells; `clamp(24px,4vw,56px)` on project cards; `9999px` on buttons; `0` on section boundaries
- **First viewport:** Poster, not document. Hero occupies 100vh with portrait anchored at bottom.

## Motion

**Approach:** Expressive — animation is this portfolio's main differentiator. The site feels kinetic because every state change is choreographed.

**Guiding rule:** Animations reveal content cinematically, they don't bury it. Every animated element must be fully readable at rest.

### Animation Inventory

| Layer | Spec | Library |
|---|---|---|
| Page entrance (nav, hero text, portrait) | opacity 0→1, translateY 40px→0, 0.7s ease-out, staggered 0.15s | GSAP |
| Scroll-reveal (about, exp, skills, contact) | opacity 0→1, translateY 40px→0, `once:true`, `start:'top 85–88%'` | GSAP ScrollTrigger |
| About text character-reveal | opacity 0.2→1 per span, scroll-progress driven | GSAP ScrollTrigger |
| Experience timeline line | height 0→100%, scrub:true | GSAP ScrollTrigger |
| Experience item hover | `padding-left: .75rem`, 250ms ease | CSS |
| Service item hover | `padding-left: .75rem`, opacity 0.85, 250ms ease | CSS |
| Project card stack | scale 0.9 per depth, sticky positioning | GSAP ScrollTrigger |
| Project card hover | border-color brightens, box-shadow adds, 300ms ease | CSS |
| Portrait float | `translateY(-18px) rotate(.7deg) scale(1.015)`, 6s ease-in-out infinite | CSS keyframes |
| Portrait glow pulse | teal drop-shadow 20px→80px, 4s ease-in-out infinite | CSS keyframes |
| Portrait magnet | spring stiffness:120 damping:14 mass:1, `pointer:coarse` disabled | motion library |
| Marquee | dual-row scroll, speed tied to page scroll direction | CSS + JS |
| Skill badges | opacity 0→1, scale 0.8→1, stagger 0.05s | GSAP |

### Timing Reference
| Name | Duration | Use |
|---|---|---|
| Micro | 150–200ms | Button hover, opacity |
| Short | 250–300ms | Card hover, item hover |
| Medium | 500–700ms | Entrance animations |
| Long | 4–6s | Float, glow pulse (infinite) |

**Easing:** `ease-out` on entrances, `ease-in-out` on loops, spring physics on interactive magnet.

**Reduced motion:** All GSAP animations, CSS keyframes, and the motion spring are gated behind `prefers-reduced-motion: reduce`. Elements snap to final state instantly.

## Intentional Design Risks

These are deliberate departures from iOS developer portfolio conventions. They are features, not bugs.

1. **Kanit** over Inter/system-ui — signals design confidence. Cost: slightly harder at 14px on low-res screens. Accepted.
2. **Wild CTA gradient** (`magenta → purple → amber`) — the contact button deliberately ignores the teal system. It is unmissable and creates a brand signature moment. Kept as a single-use pattern; do not apply elsewhere.
3. ~~White services section~~ — **removed 2026-05-15.** Was a jarring contrast break against the dark aesthetic. Services section now uses the standard dark palette with teal service numbers.

## Component Patterns

### Buttons
- **Primary (`.btn-contact`):** CTA gradient, 9999px radius, uppercase Kanit 500, `letter-spacing:.15em`, white outline inset
- **Ghost (`.btn-ghost`):** `2px solid #D7E2EA`, transparent fill, same type treatment as primary
- Hover: `opacity:.85` on primary, `background:rgba(215,226,234,.1)` on ghost

### Project Cards
- Background `#0C0C0C`, border `2px solid #D7E2EA`, radius `clamp(24px,4vw,56px)`
- Stack: `position:sticky`, `transform-origin:top center`, scales 0.9 per depth
- Number: Kanit 900, gradient text
- Images: `object-fit:cover`, `border-radius:clamp(14px,2.5vw,40px)`, `loading:lazy`

### Experience Items
- Two-column grid: `160px 1fr` (collapses to single column at 600px)
- Divider: `1px solid rgba(215,226,234,.1)` bottom only
- Hover: slide right `padding-left:.75rem`

## Decisions Log

| Date | Decision | Rationale |
|---|---|---|
| 2026-05-12 | Initial design direction set | office-hours session — dark cinematic, Three.js hero chosen for max impressiveness |
| 2026-05-12 | Kanit font chosen | Design template (Jack 3D Creator) — retained because it signals design confidence |
| 2026-05-15 | Design review audit completed | 7 findings addressed: a11y, touch targets, reduced-motion, project images, hero portrait |
| 2026-05-15 | motion library added | Spring physics for portrait magnet — replaces CSS ease-out, adds overshoot and settle |
| 2026-05-15 | Services section darkened | Risk 2 resolved — white contrast break removed, teal service numbers added |
| 2026-05-15 | DESIGN.md created | /design-consultation — formalizing the system built during the hackathon session |
| 2026-05-15 | /design-review audit run | 4 bugs found and fixed: hero portrait 404 (`.jpeg`→`.jpg`), experience heading truncated (section restructured to full-width so heading can span 915px), about text invisible (character spans had `white-space:pre` preventing wrapping — scrollWidth was 2407px), vignette color mismatch (`#080810`→`#0C0C0C`) |
