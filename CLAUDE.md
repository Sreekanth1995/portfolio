# Sreekanth Mekala — iOS Developer Portfolio

## Project Overview

Personal portfolio site for **Sreekanth Mekala**, Senior iOS Developer at JPMorgan Chase. Single-file vanilla HTML portfolio with cinematic scroll animations.

- **Entry point:** `index.html` (served via `python3 -m http.server 3000`)
- **Theme:** Dark (`#0C0C0C` background)
- **Font:** Kanit (Google Fonts, weights 300–900)
- **Design system:** See [DESIGN.md](DESIGN.md) — read this before making any visual changes

## Tech Stack

- Vanilla HTML5 + CSS3 + JavaScript (no build system, no framework)
- GSAP 3.12.5 + ScrollTrigger (CDN)
- motion 12.38.0 (CDN) — spring physics for portrait magnet
- UI/UX Pro Max skill installed at `.claude/skills/ui-ux-pro-max/`

## Section Order

1. **Hero** — full-viewport, nav, gradient heading, 3D portrait with float animation + magnet effect
2. **Marquee** — 21 GIFs scrolling left/right based on scroll position
3. **About** — character-by-character animated paragraph
4. **Experience** — timeline with stagger reveal (5 roles, newest first)
5. **Skills** — badge grid with stagger
6. **Projects** — 4 sticky-stacking project cards (JPMC, WSAudiology, MouriTech, Talview)
7. **Contact** — email + LinkedIn + GitHub + resume download

## Key Files

| File | Purpose |
|------|---------|
| `index.html` | Entire site — HTML, CSS (inline `<style>`), JS (inline `<script>`) |
| `img/projects/hero.jpeg` | 3D character portrait (animated with CSS float + glow) |
| `img/projects/01-jpmc-*.png` | 3 project images for JPMorgan Chase card |
| `img/projects/02-wsa-*.png` | 2 project images for WSAudiology card |
| `img/projects/03-mt-*.png` | 2 project images for MouriTech card |
| `img/projects/04-talview-*.png` | 2 images: 9:16 phone + 4:3 iPad (phone-ipad layout) |
| `sreekanth_resume.pdf` | Linked from contact section |
| `DESIGN.md` | Formal design system — source of truth for all visual decisions |

## Design System
Always read DESIGN.md before making any visual or UI decisions.
All font choices, colors, spacing, animation specs, and aesthetic direction are defined there.
Do not deviate without explicit user approval.

## Skill routing

When the user's request matches an available skill, invoke it via the Skill tool. When in doubt, invoke the skill.

Key routing rules:
- Product ideas/brainstorming → invoke /office-hours
- Strategy/scope → invoke /plan-ceo-review
- Architecture → invoke /plan-eng-review
- Design system/plan review → invoke /design-consultation or /plan-design-review
- Full review pipeline → invoke /autoplan
- Bugs/errors → invoke /investigate
- QA/testing site behavior → invoke /qa or /qa-only
- Code review/diff check → invoke /review
- Visual polish → invoke /design-review
- Ship/deploy/PR → invoke /ship or /land-and-deploy
- Save progress → invoke /context-save
- Resume context → invoke /context-restore

## gstack (REQUIRED — global install)

**Before doing ANY work, verify gstack is installed:**

```bash
test -d ~/.claude/skills/gstack/bin && echo "GSTACK_OK" || echo "GSTACK_MISSING"
```

If GSTACK_MISSING: STOP. Do not proceed. Tell the user:

> gstack is required for all AI-assisted work in this repo.
> Install it:
> ```bash
> git clone --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
> cd ~/.claude/skills/gstack && ./setup --team
> ```
> Then restart your AI coding tool.

Do not skip skills, ignore gstack errors, or work around missing gstack.

Using gstack skills: After install, skills like /qa, /ship, /review, /investigate,
and /browse are available. Use /browse for all web browsing.
Use ~/.claude/skills/gstack/... for gstack file paths (the global path).
