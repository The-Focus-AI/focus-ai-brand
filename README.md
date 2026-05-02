# Focus.AI Design System

A comprehensive design system skill for AI coding agents. Combines Swiss International Style structural rigor with Focus.AI brand identity across two sub-brands.

**Version 2.0.0**

## Sub-Brands

| Brand      | Aesthetic                 | Accent Colors                             | Use For                               |
| ---------- | ------------------------- | ----------------------------------------- | ------------------------------------- |
| **Client** | Editorial magazine        | Petrol `#0e3b46` + Vermilion `#c3471d`    | Services, proposals, client work      |
| **Labs**   | Bell Labs research report | Rand-Blue `#0055aa` + Alert-Red `#d93025` | Research, experiments, public content |

## What's Included

### Skill (`skills/focus-ai-brand/`)

| File                            | Purpose                                                        |
| ------------------------------- | -------------------------------------------------------------- |
| `SKILL.md`                      | Entry point — principles, quick reference, file routing        |
| `references/design-system.md`   | Colors, type scale, opacity hierarchy, spacing, dark mode      |
| `references/grid-and-layout.md` | 12-column grid + asymmetric editorial layout                   |
| `references/responsive.md`      | Mobile-first breakpoints, fluid type, touch targets            |
| `references/components.md`      | Tailwind component patterns — buttons, cards, nav, forms, hero |
| `references/tailwind-config.md` | Paste-ready Tailwind v3/v4 configs, Astro integration          |
| `references/print.md`           | `/report` command, paged.js smart page breaks, PDF workflow    |
| `references/presentations.md`   | `/deck` command, PptxGenJS slide masters, slide patterns       |
| `references/imagery.md`         | AI image generation styles (5 Client + 4 Labs)                 |
| `references/voice.md`           | Voice & tone, anti-patterns, example transformations           |
| `references/checklist.md`       | 70+ item pre-ship audit checklist                              |

### Templates (`templates/`)

| File                       | Purpose                                                     |
| -------------------------- | ----------------------------------------------------------- |
| `client-report.html`       | Client brand — standard browser printing                    |
| `client-report-paged.html` | Client brand — paged.js with running headers + page numbers |
| `labs-report.html`         | Labs brand — standard browser printing                      |
| `labs-report-paged.html`   | Labs brand — paged.js with running headers + page numbers   |

### Assets

- `assets/fonts/` — Brand typography: CinaGEO, Hypertext Mono, Ghostly Gothic
- `assets/examples/` — HTML implementation examples (landing page, hero, cards)
- `output/` — Renaissance visual style reference images

## Design Principles

1. **Grid first** — 12-column grid or asymmetric editorial. 8px base unit.
2. **Mobile first** — Design for 320px, expand with breakpoints.
3. **Whitespace is structure** — Generous spacing is the design, not waste.
4. **Opacity creates hierarchy** — Never introduce different hues for text weight.
5. **Two accents maximum** — Primary for CTAs, secondary used sparingly.
6. **Clarity over decoration** — Every element earns its place.

## Typography

| Family  | Font           | Role                                          |
| ------- | -------------- | --------------------------------------------- |
| Display | Source Serif 4 | Cover titles, H1 (paged reports), pull quotes |
| Sans    | Inter          | Headings, body text, UI                       |
| Mono    | Courier Prime  | Labels, metadata, code                        |

## Commands

```
# Generate PDF report
/report file:./document.md style:labs
/report file:./proposal.md style:client output:./proposal.pdf

# Generate presentation
/deck file:./content.md style:client output:./presentation.pptx
```

## Installation

### As a pi skill

Copy `skills/focus-ai-brand/` to your project's `.pi/skills/` directory:

```bash
cp -r skills/focus-ai-brand /path/to/your/project/.pi/skills/
```

## License

Copyright The Focus AI. All rights reserved.
