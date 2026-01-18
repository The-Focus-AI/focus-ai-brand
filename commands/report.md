---
name: report
description: Convert a markdown file to a styled HTML report using Focus.AI brand (Client or Labs) and open in browser for PDF printing
arguments:
  - name: file
    description: Path to the markdown file to convert
    required: true
  - name: style
    description: Brand style to use (client or labs)
    required: false
    default: labs
---

# Focus.AI Report Generator

Convert a markdown file to a beautifully styled HTML report and open it in the browser for printing to PDF.

## Instructions

1. Read the markdown file specified by the user: `$ARGUMENTS.file`
2. Determine the style to use: `$ARGUMENTS.style` (defaults to "labs")
3. Read the appropriate HTML template:
   - For "client": Read `${CLAUDE_PLUGIN_ROOT}/templates/client-report.html`
   - For "labs": Read `${CLAUDE_PLUGIN_ROOT}/templates/labs-report.html`

4. Convert the markdown content to HTML, applying the appropriate brand styling:

### For Labs Style:
- Use the Labs color palette: Paper (#f3f2ea), Void (#1a1a1a), Rand-Blue (#0055aa), Alert-Red (#d93025)
- Use Inter for body text (font-weight 400, 16px, line-height 1.6)
- Use Inter Black (900) for headings
- Use Courier Prime for metadata and code
- Apply the characteristic offset shadow to the main container
- H2 headers should be uppercase
- Use Alert-Red for decorative numbering

### For Client Style:
- Use the Client color palette: Paper (#faf9f6), Ink (#161616), Petrol (#0e3b46), Vermilion (#c3471d)
- Use Inter for body text (font-weight 500, 17px, line-height 1.6)
- Use Inter Bold (700) for headings with negative letter-spacing
- Use Courier Prime for labels
- Headings use negative letter-spacing (-0.045em for H1)

5. Generate a **self-contained HTML file** with:
   - All CSS embedded in a `<style>` tag (no external stylesheets)
   - Google Fonts import for Inter and Courier Prime
   - Proper print styles for PDF generation
   - Responsive layout that works well on screen and print

6. Write the HTML file to `/tmp/focus-report-{timestamp}.html`

7. Open the file in the default browser using: `open /tmp/focus-report-{timestamp}.html`

8. Tell the user:
   - The file has been opened in their browser
   - They can print to PDF using Cmd+P (or Ctrl+P)
   - The file path in case they want to access it again

## HTML Template Structure

The generated HTML should follow this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{Document Title}</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Courier+Prime:wght@400;700&family=Inter:wght@400;500;600;700;900&display=swap" rel="stylesheet">
  <style>
    /* Reset and base styles */
    /* Brand-specific styles based on client/labs */
    /* Print styles */
  </style>
</head>
<body>
  <main class="report">
    <!-- Converted markdown content -->
  </main>
</body>
</html>
```

## Print Optimization

The template includes comprehensive print styles for clean PDF output:

### White Background for Print
When printing, the background switches to white (not cream) for better compatibility:

```css
@media print {
  body {
    background: white !important;
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }
  .report {
    background: white !important;
    box-shadow: none;
    border: none;
    padding: 0.5in;
  }
  code { background: #eee !important; }
  tr:nth-child(even) td { background: #f5f5f5 !important; }
}
```

### Page Break Controls
Use these CSS classes to control page breaks:

- `.page-break` - Force a page break before the element
- `.keep-together` - Prevent the element from being split across pages

Example usage in the generated HTML:
```html
<!-- Force new page before a section -->
<div class="page-break"></div>
<h2>New Section</h2>

<!-- Keep a table or list together -->
<div class="keep-together">
  <h3>Important Table</h3>
  <table>...</table>
</div>
```

### Automatic Page Break Avoidance
The template automatically avoids breaking:
- After headings (h1-h6)
- Inside tables, code blocks, blockquotes
- Inside lists (ul, ol)
- Inside images (with max-height: 4.5in)

### Orphan/Widow Control
Paragraphs require at least 3 lines at page top/bottom to prevent awkward single-line breaks.

### Image Sizing
Images are limited to max-height: 4.5in in print to prevent overflow. The grayscale filter is removed for print.

## Example Usage

User runs: `/report file:./my-analysis.md style:labs`

Result: Opens a beautifully styled Labs-branded HTML document in the browser, ready for PDF printing.
