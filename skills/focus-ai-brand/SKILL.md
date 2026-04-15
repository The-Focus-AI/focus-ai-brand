---
name: focus-ai-brand
description: Apply Focus.AI brand guidelines to documents, presentations, websites, and other materials. Supports two sub-brands - Focus.AI Client (services, proposals, client work) and Focus.AI Labs (research, experiments, public content). Use when creating branded materials, applying visual identity, or generating content that needs to follow Focus.AI style. Trigger on "focus.ai style", "focus brand", "labs style", or requests for branded Focus.AI materials.
---

# Focus.AI Brand System

This skill applies Focus.AI brand guidelines to create consistent, on-brand materials across two sub-brands.

## Required Reading

**IMPORTANT**: Before creating any branded material, you MUST read the appropriate design system files:

### For ALL Brand Work
First, read the shared foundations:
```
Read: ${CLAUDE_PLUGIN_ROOT}/THEFOCUS_DESIGN_SYSTEM.md
```

### Then, Based on Context

**For Client Materials** (proposals, case studies, client work, service pages):
```
Read: ${CLAUDE_PLUGIN_ROOT}/THEFOCUS_CLIENT_DESIGN_SYSTEM.md
```

**For Labs Materials** (research, experiments, blog posts, open source):
```
Read: ${CLAUDE_PLUGIN_ROOT}/THEFOCUS_LABS_DESIGN_SYSTEM.md
```

## Brand Selection Guide

| Context | Brand | Design System File |
|---------|-------|-------------------|
| Client proposals | Client | THEFOCUS_CLIENT_DESIGN_SYSTEM.md |
| Case studies | Client | THEFOCUS_CLIENT_DESIGN_SYSTEM.md |
| Service pages | Client | THEFOCUS_CLIENT_DESIGN_SYSTEM.md |
| Product marketing | Client | THEFOCUS_CLIENT_DESIGN_SYSTEM.md |
| Conference analysis | Labs | THEFOCUS_LABS_DESIGN_SYSTEM.md |
| Research reports | Labs | THEFOCUS_LABS_DESIGN_SYSTEM.md |
| Experiments | Labs | THEFOCUS_LABS_DESIGN_SYSTEM.md |
| Technical blog posts | Labs | THEFOCUS_LABS_DESIGN_SYSTEM.md |
| Open source projects | Labs | THEFOCUS_LABS_DESIGN_SYSTEM.md |

**Rule of thumb**: Client work or selling services → Client brand. Sharing learnings or exploring → Labs brand.

## Quick Difference Summary

| Aspect | Client | Labs |
|--------|--------|------|
| **Aesthetic** | Magazine / editorial | Bell Labs / RAND Corporation |
| **Primary accent** | Petrol `#0e3b46` | Rand-Blue `#0055aa` |
| **Secondary accent** | Vermilion `#c3471d` | Alert-Red `#d93025` |
| **Voice** | Confident, professional, clear | Curious, wry, generous |

## Workflow

1. **Determine brand**: Client work → Client brand. Research/sharing → Labs brand.
2. **Read foundations**: Load `THEFOCUS_DESIGN_SYSTEM.md`
3. **Read brand specifics**: Load the appropriate brand file (Client or Labs)
4. **Apply guidelines**: Follow typography, colors, layout, and voice from the loaded files
5. **Verify**: Check against the quality checklist in the design system files

## Commands

### `/report` - Generate Report / PDF

Convert a markdown file to a styled HTML report. Two modes:

```
# Open in browser for manual Cmd+P printing
/report file:./my-document.md style:labs

# Generate PDF directly via chrome-driver (uses paged.js template)
/report file:./proposal.md style:client output:./proposal.pdf

# Force paged template in browser
/report file:./analysis.md style:client paged:true
```

**Arguments:**
- **file**: Path to the markdown file (required)
- **style**: `client` or `labs` (default: labs)
- **output**: PDF output path — when specified, generates PDF directly and uses paged template
- **paged**: `auto` (default) / `true` / `false` — controls paged.js template selection

**Paged templates** provide:
- Running "THEFOCUS.AI" header on every page (except cover)
- Auto page numbers (01, 02, ...) in Courier Prime
- Source Serif 4 display font for titles and cover pages
- Cream background preserved in PDF
- Smart page breaks: each h2 section starts on a new page
- Component library for rich layouts (cards, stat grids, process flows, etc.)

**Standard templates** are simpler — no running headers, no paged.js, designed for Cmd+P browser printing.

## Typography

Three font families:

| Family | Font | Usage |
|--------|------|-------|
| **Display** | Source Serif 4 | Cover titles, H1 (paged reports), pull quotes, stat numbers |
| **Sans** | Inter | Section headings (h2-h4), body text, UI |
| **Mono** | Courier Prime | Labels, metadata, code, page numbers |

Source Serif 4 is **paged reports only** — standard templates use Inter for everything.

## Assets

- `${CLAUDE_PLUGIN_ROOT}/templates/` — HTML report templates
  - `client-report.html` / `labs-report.html` — Standard (browser printing)
  - `client-report-paged.html` / `labs-report-paged.html` — Paged.js (PDF generation)
- `${CLAUDE_PLUGIN_ROOT}/assets/fonts/` — Font files
- `${CLAUDE_PLUGIN_ROOT}/assets/examples/` — HTML implementation examples
