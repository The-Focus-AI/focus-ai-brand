# Focus.AI Brand Plugin for Claude Code

A Claude Code skill plugin that applies Focus.AI brand guidelines to documents, presentations, websites, and other materials.

## Overview

This plugin provides comprehensive brand guidelines for two Focus.AI sub-brands:

- **Focus.AI Client**: For services, proposals, client work, and product marketing
- **Focus.AI Labs**: For research, experiments, blog posts, and open source projects

## Installation

Install this plugin in Claude Code by adding it to your plugins directory:

```bash
# Clone the repository
git clone https://github.com/The-Focus-AI/focus-ai-brand.git

# Move to your Claude Code plugins directory
mv focus-ai-brand ~/.claude/plugins/
```

## Usage

The skill automatically triggers when you:

- Request "focus.ai style" or "focus brand" materials
- Ask for "labs style" content
- Create branded Focus.AI materials

Claude will automatically read the appropriate design system files and apply the correct brand guidelines based on your context.

## What's Included

### Design Systems

- `THEFOCUS_DESIGN_SYSTEM.md` - Shared brand foundations (typography, principles, quality standards)
- `THEFOCUS_CLIENT_DESIGN_SYSTEM.md` - Client brand specifics (magazine/editorial aesthetic)
- `THEFOCUS_LABS_DESIGN_SYSTEM.md` - Labs brand specifics (research/technical aesthetic)

### Assets

- **Fonts** (`assets/fonts/`) - Brand typography files including:
  - Cina GEO (Regular, Medium, Bold, Light)
  - Hypertext Mono (Light, Medium, Bold)
  - Ghostly Gothic Test (Light)

- **Examples** (`assets/examples/`) - HTML implementation examples:
  - Full landing page
  - Hero sections
  - Card components

## Brand Selection Guide

| Context | Brand to Use |
|---------|--------------|
| Client proposals, case studies, service pages | **Client** brand |
| Research reports, experiments, technical blogs | **Labs** brand |

**Rule of thumb**: Client work or selling services → Client brand. Sharing learnings or exploring → Labs brand.

## Quick Difference Summary

| Aspect | Client | Labs |
|--------|--------|------|
| **Aesthetic** | Magazine / editorial | Bell Labs / RAND Corporation |
| **Primary accent** | Petrol `#0e3b46` | Rand-Blue `#0055aa` |
| **Secondary accent** | Vermilion `#c3471d` | Alert-Red `#d93025` |
| **Voice** | Confident, professional, clear | Curious, wry, generous |

## Development

This is a Claude Code plugin following the standard plugin structure:

```
focus-ai-brand/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── skills/
│   └── focus-ai-brand.md    # Main skill definition
├── assets/
│   ├── fonts/               # Brand typography
│   └── examples/            # HTML examples
├── THEFOCUS_DESIGN_SYSTEM.md
├── THEFOCUS_CLIENT_DESIGN_SYSTEM.md
├── THEFOCUS_LABS_DESIGN_SYSTEM.md
└── README.md
```

## License

Copyright The Focus AI. All rights reserved.

## Support

For issues or questions about this plugin, please contact The Focus AI team.
