---
name: report
description: Convert a markdown file to a styled HTML report using Focus.AI brand (Client or Labs) and open in browser or generate PDF directly
arguments:
  - name: file
    description: Path to the markdown file to convert
    required: true
  - name: style
    description: Brand style to use (client or labs)
    required: false
    default: labs
  - name: output
    description: PDF output path. If specified, generates PDF directly via chrome-driver instead of opening browser
    required: false
  - name: paged
    description: Use paged.js template with running headers, page numbers, and component library (auto/true/false). Defaults to auto — uses paged when output is specified
    required: false
    default: auto
---

# Focus.AI Report Generator

Convert a markdown file to a beautifully styled HTML report. Can open in browser for manual printing, or generate PDF directly via chrome-driver.

## Instructions

1. Read the markdown file specified by the user: `$ARGUMENTS.file`
2. Determine the style to use: `$ARGUMENTS.style` (defaults to "labs")
3. Determine if paged template should be used:
   - `$ARGUMENTS.paged` = "true" → use paged template
   - `$ARGUMENTS.paged` = "false" → use standard template
   - `$ARGUMENTS.paged` = "auto" (default) → use paged if `$ARGUMENTS.output` is specified, otherwise standard
4. Read the appropriate HTML template from `${CLAUDE_PLUGIN_ROOT}/templates/`:

   | Style | Standard | Paged |
   |-------|----------|-------|
   | client | `client-report.html` | `client-report-paged.html` |
   | labs | `labs-report.html` | `labs-report-paged.html` |

5. Convert the markdown content to HTML, applying the appropriate brand styling.

### Page Break Conventions (Paged templates only)

When generating HTML for paged templates, follow these rules for clean pagination:

1. **Every `h2` automatically starts on a new page** (`break-before: page` is in the CSS). The first h2 after the cover/stat-grid should have class `no-break-before` to avoid a wasted blank page.

2. **Wrap `h3` + its following content** in `<div class="section">` to keep them together. This prevents a heading from orphaning at the bottom of a page while its content flows to the next.

3. **All components are protected** — cards, grids, callouts, process flows, tables, checklists all have `break-inside: avoid`. No need for extra wrappers.

4. **Use `<div class="page-break"></div>`** for manual page breaks when needed (e.g., before a full-page diagram).

5. **Document structure should be**: cover → optional stat-grid → first h2 (`.no-break-before`) → content → h2 → content → h2 → content → footer. Each h2 section becomes its own "chapter" starting at the top of a page.

### Component Syntax (Paged templates only)

When using paged templates, recognize these HTML patterns in the markdown and convert them to the appropriate CSS classes:

```html
<!-- Cover page (must be first element) -->
<section class="cover">
  <div class="brand-mark">THEFOCUS.AI</div>
  <h1>Report Title</h1>
  <div class="subtitle">A brief description of the report</div>
  <div class="cover-rule"></div>
  <div class="cover-meta">
    <strong>Prepared for:</strong> Client Name<br>
    <strong>Date:</strong> April 2026<br>
    <strong>Author:</strong> Will Schenk
  </div>
</section>

<!-- Two-column layout -->
<div class="two-col">
  <div>Left column content</div>
  <div>Right column content</div>
</div>

<!-- Asymmetric columns -->
<div class="two-col-wide-left">...</div>
<div class="two-col-wide-right">...</div>

<!-- Cards -->
<div class="card-dark">Dark petrol/void card with white text</div>
<div class="card-light">Light card with primary accent border</div>
<div class="card-accent">Accent card with vermilion/red border</div>

<!-- Stat blocks -->
<div class="stat-grid">
  <div>
    <div class="stat-number">42%</div>
    <div class="stat-label">Improvement</div>
  </div>
  <div>
    <div class="stat-number">3.2x</div>
    <div class="stat-label">Faster</div>
  </div>
  <div>
    <div class="stat-number">$1.2M</div>
    <div class="stat-label">Saved</div>
  </div>
</div>

<!-- Callouts -->
<div class="callout">Light callout for notes or context</div>
<div class="callout-key">Dark callout for key takeaways</div>

<!-- Process flow -->
<div class="process-flow">
  <div class="step">
    <div class="step-number">Step 01</div>
    <div class="step-title">Discover</div>
    <div class="step-desc">Identify data sources</div>
  </div>
  <div class="step">
    <div class="step-number">Step 02</div>
    <div class="step-title">Connect</div>
    <div class="step-desc">Build integrations</div>
  </div>
  <div class="step">
    <div class="step-number">Step 03</div>
    <div class="step-title">Deliver</div>
    <div class="step-desc">Deploy interfaces</div>
  </div>
</div>

<!-- Pull quote -->
<div class="pull-quote">
  This is a display quote using Source Serif 4.
  <cite>— Attribution</cite>
</div>

<!-- Page break -->
<div class="page-break"></div>
```

### For Labs Style:
- Use the Labs color palette: Paper (#f3f2ea), Void (#1a1a1a), Rand-Blue (#0055aa), Alert-Red (#d93025)
- Use Inter for body text (font-weight 400, 15px, line-height 1.6)
- Use Inter Black (900) for headings
- Use Source Serif 4 (900) for h1 and cover title (paged only)
- Use Courier Prime for metadata and code
- H2 headers are uppercase with auto-numbering
- Use Alert-Red for decorative numbering and accents

### For Client Style:
- Use the Client color palette: Paper (#faf9f6), Ink (#161616), Petrol (#0e3b46), Vermilion (#c3471d)
- Use Inter for body text (font-weight 500, 15px, line-height 1.6)
- Use Inter Bold (700) for headings with negative letter-spacing
- Use Source Serif 4 (900) for h1 and cover title (paged only)
- Use Courier Prime for labels
- Headings use negative letter-spacing

6. Generate a **self-contained HTML file** with:
   - All CSS embedded in a `<style>` tag
   - Google Fonts import for Inter, Courier Prime, and Source Serif 4 (paged templates)
   - Paged.js script tags with font-safe initialization (paged templates)
   - The content placed inside `<body>` directly (paged) or inside `<main class="report">` (standard)

7. Write the HTML file to `/tmp/focus-report-{timestamp}.html`

8. **If `$ARGUMENTS.output` is specified**, generate PDF directly.

   First, find the chrome-driver pdf binary. Look for it at:
   - `${CLAUDE_PLUGIN_ROOT}/../../../chrome-driver/*/bin/pdf` (sibling plugin in same cache)
   - Or find the latest version: `ls -d ~/.claude/plugins/cache/focus-marketplace/chrome-driver/*/bin/pdf | sort -V | tail -1`

   Then run:
   ```bash
   <chrome-driver-pdf-path> \
     file:///tmp/focus-report-{timestamp}.html \
     $ARGUMENTS.output
   ```
   Report the output path and file size.

9. **If no output specified**, open in browser:
   ```bash
   open /tmp/focus-report-{timestamp}.html
   ```
   Tell the user:
   - The file has been opened in their browser
   - They can print to PDF using Cmd+P
   - The file path in case they want to access it again

## HTML Template Structure

### Standard Templates (browser printing)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{Document Title}</title>
  <link href="https://fonts.googleapis.com/css2?family=Courier+Prime:wght@400;700&family=Inter:wght@400;500;600;700;900&display=swap" rel="stylesheet">
  <style>/* Brand-specific styles + print styles */</style>
</head>
<body>
  <main class="report">
    <!-- Converted markdown content -->
  </main>
</body>
</html>
```

### Paged Templates (chrome-driver PDF generation)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{Document Title}</title>
  <link href="https://fonts.googleapis.com/css2?family=Courier+Prime:wght@400;700&family=Inter:wght@400;500;600;700;900&family=Source+Serif+4:ital,opsz,wght@0,8..60,400;0,8..60,700;0,8..60,900;1,8..60,400&display=swap" rel="stylesheet">
  <style>/* @page rules, component library, brand styles */</style>
  <script>window.PagedConfig = { auto: false };</script>
  <script src="https://unpkg.com/pagedjs/dist/paged.polyfill.js"></script>
  <script>document.fonts.ready.then(() => window.PagedPolyfill.preview());</script>
</head>
<body>
  <section class="cover">...</section>
  <!-- Converted markdown content -->
</body>
</html>
```

## Paged Template Features

When using paged templates, these features are available:

### Running Headers & Page Numbers
- **THEFOCUS.AI** (or THEFOCUS.AI LABS) appears top-left in vermilion/red on every page except the cover
- Page numbers (01, 02, etc.) appear top-right in Courier Prime
- Cover page suppresses both headers and page numbers

### Cream Background in Print
- The warm paper background (#faf9f6 or #f3f2ea) is preserved in the PDF
- No white background override — the cream is part of the brand

### Display Typography
- H1 and cover titles use Source Serif 4 at weight 900 — a bold serif for impact
- All other text remains Inter/Courier Prime
- Pull quotes use Source Serif 4 italic

### Component Library
Available CSS classes for rich layouts:

| Component | Class | Description |
|-----------|-------|-------------|
| Two-column | `.two-col` | Equal 2-col grid |
| Wide left | `.two-col-wide-left` | 3fr / 2fr grid |
| Wide right | `.two-col-wide-right` | 2fr / 3fr grid |
| Dark card | `.card-dark` | Primary dark card (petrol/void bg) |
| Light card | `.card-light` | Bordered, primary accent left border |
| Accent card | `.card-accent` | Bordered, secondary accent left border |
| Stat number | `.stat-number` | 48px display serif number |
| Stat label | `.stat-label` | 11px mono label in accent color |
| Stat grid | `.stat-grid` | 3-column stat layout |
| Callout | `.callout` | Light background callout |
| Key callout | `.callout-key` | Dark background callout |
| Process flow | `.process-flow` | Horizontal step sequence with arrows |
| Pull quote | `.pull-quote` | Display serif italic with attribution |
| Section wrap | `.section` | Keeps h3 + its content together (break-inside: avoid) |
| No break before | `.no-break-before` | Suppress h2 auto page break (use on first h2) |
| Page break | `.page-break` | Force page break |
| Keep together | `.keep-together` | Prevent splitting across pages |

## Example Usage

```
# Standard: open in browser
/report file:./analysis.md style:labs

# Paged: generate PDF directly
/report file:./analysis.md style:client output:./analysis.pdf

# Force paged template but open in browser
/report file:./analysis.md style:client paged:true
```
