# The Focus.AI Client Design System

> For client-facing work: services, products, proposals, case studies, marketing
>
> **Prerequisites**: Read [THEFOCUS_DESIGN_SYSTEM.md](./THEFOCUS_DESIGN_SYSTEM.md) for shared foundations.

---

## Brand Overview

**Focus.AI (Client)** is the professional services brand — polished, editorial, confident. This is what clients see when evaluating Focus.AI as a partner.

### Tagline
**"Distill the signal from the noise"**

### Aesthetic
Editorial magazine meets technology consultancy. Think: well-designed business publication, not generic SaaS marketing.

### Audience
Organizations seeking AI transformation — executives, technical leaders, decision-makers evaluating partners.

---

## Color System

### Primary Palette

| Color | Hex | CSS Variable | Usage |
|-------|-----|--------------|-------|
| **Paper** | `#faf9f6` | `--color-paper` | Primary background |
| **Ink** | `#161616` | `--color-ink` | Primary text, headings |
| **Graphite** | `#4a4a4a` | `--color-graphite` | Secondary text, muted content |
| **Petrol** | `#0e3b46` | `--color-petrol` | Primary accent, CTAs, links |
| **Vermilion** | `#c3471d` | `--color-vermilion` | Secondary accent (use sparingly) |

### Tinted Backgrounds

For section variety while maintaining warmth:

| Tint | Hex | Usage |
|------|-----|-------|
| **Cool** | `#edf6f8` | Work/services pages |
| **Sage** | `#eef6ee` | Capabilities pages |
| **Warm** | `#f7f0e6` | About pages |
| **Lavender** | `#f2eef6` | Insights/tools |
| **Aqua** | `#edf6f6` | Contact pages |

### Color Rules

1. Maximum 5 colors per composition (excluding tints)
2. Petrol is primary for actions, navigation, brand moments
3. Vermilion is accent only — use sparingly for highlights
4. No gradients — use solid colors
5. Override text colors when changing backgrounds for contrast

### Contrast Ratios

| Combination | Ratio | Pass |
|-------------|-------|------|
| Ink on Paper | 14.5:1 | AAA |
| Graphite on Paper | 6.5:1 | AA |
| Petrol on Paper | 10.2:1 | AAA |
| Vermilion on Paper | 5.8:1 | AA |

---

## Typography

### Font Application

| Element | Font | Size | Weight | Other |
|---------|------|------|--------|-------|
| **H1** | Inter | 48-88px | 700 | Letter-spacing: -0.045em |
| **H2** | Inter | 36-48px | 700 | Letter-spacing: -0.03em |
| **H3** | Inter | 24-30px | 700 | Letter-spacing: -0.02em |
| **H4** | Inter | 20px | 700 | Letter-spacing: -0.01em |
| **Body** | Inter | 17px | 500 | Line-height: 1.6 |
| **Large Body** | Inter | 20px | 500 | Line-height: 1.5 |
| **Small** | Inter | 14px | 500 | Line-height: 1.5 |
| **Label** | Courier Prime | 12px | 500 | Uppercase, letter-spacing: 0.12em |

### Mobile Typography

| Element | Mobile Size | Notes |
|---------|-------------|-------|
| **H1** | 32-56px | Use clamp() for fluid sizing |
| **H2** | 24-36px | Line-height: 1.1 |
| **Body** | 16px | Line-height: 1.65 |
| **Label** | 11px | Letter-spacing: 0.1em |

### Responsive Example

```css
h1 {
  font-size: clamp(32px, 8vw, 88px);
  font-weight: 700;
  letter-spacing: -0.045em;
  line-height: 0.95;
}
```

---

## Layout System

### Asymmetric Three-Column Grid

The signature Focus.AI layout — editorial, not generic:

```
[Label Gutter: 140px] [Content Main: 1fr, max 740px] [Marginalia: 200px]
Gap: 3rem (48px)
Max-width: 1400px
```

### CSS Implementation

```css
.asymmetric-container {
  display: grid;
  grid-template-columns: 140px 1fr 200px;
  gap: 3rem;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 2rem;
}

.label-gutter {
  /* Left column — section labels, navigation */
}

.content-main {
  max-width: 740px;
  /* Center column — primary content */
}

.marginalia-gutter {
  /* Right column — metadata, notes, secondary info */
}

/* Mobile: single column */
@media (max-width: 1024px) {
  .asymmetric-container {
    grid-template-columns: 1fr;
    gap: 1.5rem;
    padding: 0 1.25rem;
  }
}
```

### Section Spacing

| Context | Desktop | Mobile |
|---------|---------|--------|
| Section padding (vertical) | 7rem (112px) | 3rem (48px) |
| Container padding (horizontal) | 2rem (32px) | 1.25rem (20px) |
| Between major sections | 8rem | 4rem |

---

## Component Patterns

### Primary CTA Button

```html
<a href="#" class="cta-primary">
  Get Started
  <svg><!-- arrow icon --></svg>
</a>
```

```css
.cta-primary {
  font-family: 'Courier Prime', monospace;
  font-size: 12px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.15em;
  padding: 0.875rem 1.5rem;
  border: 1px solid var(--petrol);
  background: transparent;
  color: var(--petrol);
  border-radius: 6px;
  transition: all 200ms cubic-bezier(0.4, 0, 0.2, 1);
}

.cta-primary:hover {
  background: rgba(14, 59, 70, 0.04);
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(14, 59, 70, 0.1);
}

.cta-primary svg {
  transition: transform 200ms;
}

.cta-primary:hover svg {
  transform: translateX(4px);
}
```

### Cards

**Standard Card:**
```css
.card {
  background: var(--paper);
  border: 1px solid #d4d3cf;
  border-radius: 8px;
  padding: 2rem;
  transition: transform 300ms, box-shadow 300ms;
}

.card:hover {
  transform: translateX(4px);
  box-shadow: 0 4px 16px rgba(22, 22, 22, 0.06);
}
```

**Elevated Card:**
```css
.card-elevated {
  box-shadow: 0 2px 8px rgba(22, 22, 22, 0.04);
}

.card-elevated:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(22, 22, 22, 0.08);
}
```

### Links

Midpoint underline animation:

```css
.link {
  position: relative;
  color: var(--petrol);
}

.link::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 50%;
  width: 0;
  height: 1px;
  background: var(--petrol);
  transition: width 150ms ease, left 150ms ease;
}

.link:hover::after {
  width: 100%;
  left: 0;
}
```

### Labels/Kickers

```css
.label {
  font-family: 'Courier Prime', monospace;
  font-size: 12px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--petrol);
}
```

### Dividers

```css
/* Quiet Rule */
.divider {
  height: 1px;
  background: rgba(212, 211, 207, 0.5);
}

/* Petrol accent */
.divider-accent {
  height: 1px;
  background: rgba(14, 59, 70, 0.3);
}
```

---

## Voice & Tone

### Client Voice Characteristics

- **Confident**: We know what we're doing, no hedging
- **Professional**: Polished but not stiff
- **Clear**: Direct communication, no jargon without purpose
- **Warm**: Human and approachable, not robotic

### What We Sound Like

- A trusted advisor explaining strategy
- A well-edited business publication
- A senior colleague presenting findings

### What We Don't Sound Like

- A salesperson pushing features
- Generic SaaS marketing copy
- Overly casual or trying too hard

### Writing Guidelines

**Do:**
- Lead with value, not features
- Use specific examples and outcomes
- Address the reader's challenges directly
- Be concise — respect their time

**Don't:**
- Use buzzwords without substance
- Make vague promises
- Oversell capabilities
- Use exclamation points

### Example Transformations

| Don't Write | Write Instead |
|-------------|---------------|
| "Our cutting-edge AI solutions leverage machine learning to unlock unprecedented value!" | "We connect your siloed data sources and make them accessible through natural language." |
| "Contact us to learn more about our services." | "Let's discuss how this applies to your situation." |
| "We're passionate about helping businesses succeed!" | "We help organizations find signal in their data." |

---

## Animation & Interaction

### Timing

| Duration | Usage |
|----------|-------|
| 150ms | Quick interactions (underlines, small transforms) |
| 200ms | Standard transitions (buttons, colors) |
| 300ms | Hover effects on cards |
| 600-800ms | Section reveals, fade-ins |

### Easing

```css
/* Standard */
cubic-bezier(0.4, 0, 0.2, 1)

/* Smooth */
ease
```

### Common Animations

**Fade In Up:**
```css
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in-up {
  animation: fadeInUp 800ms cubic-bezier(0.4, 0, 0.2, 1) forwards;
}
```

---

## Page Templates

### Hero Section

```html
<section class="hero">
  <div class="asymmetric-container">
    <div class="label-gutter">
      <span class="label">Services</span>
    </div>
    <div class="content-main">
      <h1>Distill the signal from the noise</h1>
      <p class="lead">We help organizations leverage AI to connect siloed data, build curated interfaces, and focus on what matters.</p>
      <a href="/contact" class="cta-primary">Start a Conversation</a>
    </div>
    <div class="marginalia-gutter">
      <!-- Optional metadata -->
    </div>
  </div>
</section>
```

### Case Study Card

```html
<article class="card">
  <span class="label">Transportation • 2024</span>
  <h3>EV Fleet Data Management</h3>
  <p>Unified disparate charging and vehicle data sources into a single queryable interface.</p>
  <a href="/case-study/ev-fleet" class="link">Read Case Study →</a>
</article>
```

---

## Renaissance Visual Style System

All Client brand generated imagery uses a **Renaissance drafting aesthetic** — inspired by Leonardo da Vinci's technical notebooks, Albrecht Dürer's engravings, and Renaissance-era scientific illustration. This connects to the brand's core values: precision, clarity, the intersection of art and science.

> **Note:** This visual style is exclusively for Client brand. Labs uses a Bell Labs / Tufte aesthetic instead. See [THEFOCUS_LABS_DESIGN_SYSTEM.md](./THEFOCUS_LABS_DESIGN_SYSTEM.md).

### The Five Approved Styles

When generating images with nano-banana (or any image generation tool) for Client work, use one of these five styles.

#### 1. Da Vinci Diagram — PRIMARY / DEFAULT

Use for: System architecture, data flows, technical explainers, general-purpose brand imagery. **This is the default** — when in doubt, use this.

**Prompt template:**
```
[Your subject/concept] drawn in the style of Leonardo da Vinci's technical notebooks.
Sepia ink on aged parchment paper. Hand-drawn construction lines, annotations in
italic script along the margins, cross-hatching for shadows. [Specific labels/callouts].
Red chalk accent marks on key intersection points. Renaissance engineering drawing
aesthetic, warm brown tones, visible paper grain texture.
```

**Key visual elements:** Interconnected nodes, Latin labels, construction geometry, gear illustrations, red chalk accents, folio-style layout.

#### 2. Dürer Engraving

Use for: Dense knowledge maps, comprehensive overviews, "big picture" or encyclopedic visuals. Best when showing the full scope of a domain or system of knowledge.

**Prompt template:**
```
[Your subject/concept] in the style of Albrecht Dürer's engravings. Extremely fine
crosshatched lines creating rich tonal depth. Woodcut and copper engraving aesthetic.
[Central element] radiates connections to surrounding elements. Meticulous detail,
black ink on off-white paper. Northern Renaissance printmaking style. Dense parallel
hatching lines for shadow. Gothic letterforms for labels.
```

**Key visual elements:** Fine crosshatching, woodcut texture, central radiating composition, figures and vignettes in surrounding panels, Gothic letterforms, dense detail.

#### 3. Celestial Map

Use for: Data architecture layers, hierarchical systems, infrastructure diagrams. Best for showing concentric layers or orbital relationships between components.

**Prompt template:**
```
[Your subject/concept] drawn in the style of Renaissance astronomical charts.
Copernicus and Kepler inspired orbital diagrams. Concentric circles showing different
layers of [your system/architecture]. Constellation-like connection lines between nodes.
Aged parchment with compass rose. Celestial cartography aesthetic, copper engraving
style with fine lines. Stars as [endpoints], orbits as [flows/relationships].
```

**Key visual elements:** Concentric orbital rings, compass rose, constellation connections, planetary nodes, star field, dimension labels, warm parchment with dark ink.

#### 4. Cartography

Use for: Network topology, connection/route maps, ecosystem visuals, marketplace diagrams. Best when showing how things connect across a landscape or territory.

**Prompt template:**
```
[Your subject/concept] in the style of Renaissance cartography and portolan charts.
A network map showing [routes/connections] like trade routes between ports. Compass
roses at intersections. Rhumb lines connecting nodes. Decorative cartouche frame.
Wind heads in corners. Aged vellum texture. Hand-drawn coastlines as [boundaries].
Sea monsters in margins representing [noise/chaos/obstacles]. Warm sepia and blue ink.
```

**Key visual elements:** Compass roses, rhumb lines, decorative cartouche, wind heads, sea monsters, port/harbor nodes, coastline boundaries, trade route connections.

#### 5. Distillation Machine

Use for: Process flows, transformation pipelines, ETL diagrams, and especially the core "distill the signal from the noise" brand narrative. Best for showing input → transformation → output.

**Prompt template:**
```
Leonardo da Vinci style technical drawing of a machine that [transforms/processes
your concept]. Intricate mechanical apparatus with gears, tubes, and chambers.
[Raw input] enters from the left as chaotic ink splatters and exits on the right
as clean organized lines. Pen and ink on aged paper with red chalk annotations.
Cross-hatching shading technique. Dimension lines and measurement marks. Small
handwritten notes in margins. Renaissance engineering patent drawing aesthetic.
```

**Key visual elements:** Mechanical apparatus, gears and tubes, alembics and chambers, chaotic input vs clean output, dimension/measurement lines, marginal annotations, fire/furnace elements.

### Style Selection Guide

| Use Case | Recommended Style |
|----------|-------------------|
| Default / general brand imagery | Da Vinci Diagram |
| System architecture overview | Da Vinci Diagram |
| Data flow or pipeline | Da Vinci Diagram or Distillation Machine |
| Knowledge domain overview | Dürer Engraving |
| Encyclopedic / comprehensive visual | Dürer Engraving |
| Layered architecture (infra, stack) | Celestial Map |
| Hierarchical / nested systems | Celestial Map |
| Network / connection map | Cartography |
| Ecosystem or marketplace visual | Cartography |
| Transformation / ETL process | Distillation Machine |
| "Distill the signal" brand story | Distillation Machine |
| Hero image / landing page | Da Vinci Diagram or Celestial Map |
| Blog post header | Any (match to content) |
| Report cover | Da Vinci Diagram or Dürer Engraving |
| Social media graphic | Da Vinci Diagram (most recognizable) |
| Client proposal | Da Vinci Diagram or Distillation Machine |
| Case study visual | Any (match to subject) |

### Visual Principles

All five styles share these characteristics:
- **Warm parchment/paper backgrounds** — never pure white or modern gradients
- **Sepia/brown ink tones** with red chalk or sanguine accents
- **Hand-drawn quality** — construction lines, cross-hatching, visible draftsmanship
- **Annotation and labeling** — marginalia, dimension marks, Latin or technical labels
- **No photography, no modern UI, no flat design** — always the Renaissance drafting aesthetic

### Reference Images

Generated examples are in `output/`:
- `output/renaissance-01-diagram.png` — Da Vinci Diagram
- `output/renaissance-07-durer.png` — Dürer Engraving
- `output/renaissance-08-celestial.png` — Celestial Map
- `output/renaissance-10-cartography.png` — Cartography
- `output/renaissance-05-distillation-machine.png` — Distillation Machine

---

## Quality Checklist

Before shipping client-facing work:

- [ ] Colors limited to Paper, Ink, Graphite, Petrol, Vermilion (+ tints)
- [ ] Inter for headings/body, Courier Prime for labels
- [ ] Negative letter-spacing on headings (-0.045em on H1)
- [ ] Asymmetric layout used where appropriate
- [ ] Labels are uppercase, 12px, Courier Prime, 0.12em spacing
- [ ] Petrol for actions, Vermilion sparingly
- [ ] Contrast ratios meet WCAG AA (4.5:1 minimum)
- [ ] Border radius is 6-8px for cards
- [ ] Hover states include subtle animations
- [ ] Voice is confident and professional, not salesy
- [ ] No buzzwords, no hyperbole
- [ ] Mobile responsive
- [ ] Generated imagery uses Renaissance visual styles (not Bell Labs/Tufte)

---

## Related Files

- [THEFOCUS_DESIGN_SYSTEM.md](./THEFOCUS_DESIGN_SYSTEM.md) — Shared foundations
- [THEFOCUS_LABS_DESIGN_SYSTEM.md](./THEFOCUS_LABS_DESIGN_SYSTEM.md) — Labs brand (different palette, different voice)
