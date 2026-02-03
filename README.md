# Design System Token Architecture

Welcome. I am the Lead Design System Engineer, and this README is the single source of truth for our design tokens.

This system uses a **Shade & Intensity-Based Naming** convention. I prioritize semantic meaning (what it does) and intensity (how strong it looks) over raw values.

---

## Core Philosophy

1. **No Raw Values**
   I never reference hex codes or pixels directly in UI components.

2. **Two Parallel Naming Layers**
   Every token exists in two forms:

* a Designer-facing name (English, Title Case, human-readable)
* a Developer-facing CSS variable (kebab-case, lowercase, double-dash prefix)

3. **Themable by Design**
   Intensity is relative. "Strong" means darker in Light Mode and lighter in Dark Mode.

---

## Token Hierarchy

I organize tokens into three layers. Data flows strictly from left to right.

```
[ Layer 1: Primitives ]      [ Layer 2: Semantic ]           [ Layer 3: Components ]
   Raw, Stable Values           Context and Intent              Implementation Use
+---------------------+      +--------------------------+     +----------------------+
| Neutral 100         | ---> | Background Surface Weak  | --> | Card                  |
| --neutral-100       |      | --color-background-      |     | Sidebar               |
|                     |      | surface-weak             |     |                       |
| Brand 600           | ---> | Interactive Primary      | --> | Primary Button        |
| --brand-600         |      | --color-interactive-     |     | CTA Links             |
|                     |      | primary                  |     |                       |
| Space 100 (8px)     | ---> | Focus Border Width       | --> | Focus ring styling    |
| --space100          |      | --border-width-focus     |     |                       |
+---------------------+      +--------------------------+     +----------------------+
           ^                            ^                              ^
    (Stable and Global)         (Theme Dependent)                (Composition)
```

---

## Designer names vs CSS variable snippets

Every token exists in two parallel forms.

* **Designer Name**
  English, Title Case, human-readable, no technical prefixes

* **CSS Variable**
  kebab-case, lowercase, double-dash prefix

I always show examples as a pair.

Examples:

* **Background Weak**: `--color-background-weak`
* **Text Strongest**: `--color-text-strongest`
* **Border Danger Weak**: `--color-border-danger-weak`
* **Shadow Focus Border**: `--shadow-focus-border`

---

## Mapping Rules

### Developer to Designer

I derive the Designer Name from the CSS variable as follows:

1. Remove the `--` prefix
2. Split by `-`
3. Convert the category prefix into a human-readable category
4. Convert remaining parts to Title Case
5. Keep numbers unchanged

Category mapping:

* `color-background` -> Background
* `color-text` -> Text
* `color-border` -> Border
* `color-icon` -> Icon
* `color-interactive` -> Interactive
* `color-data` -> Data
* `shadow` -> Shadow
* `radius` -> Radius
* `space` -> Space
* `border-width` -> Border Width

Examples:

* **Background Surface Weakest**: `--color-background-surface-weakest`
* **Interactive Primary Hover Weakest**: `--color-interactive-primary-hover-weakest`
* **Border Width 2**: `--border-width-2`

### Designer to Developer

I derive the CSS variable from the Designer Name like this:

1. Map the first word(s) back to the category prefix
2. Lowercase the rest and join with hyphens
3. Never add `-default`
4. The base token has no intensity suffix

Examples:

* **Background Primary**: `--color-background-primary`
* **Text Muted**: `--color-text-muted`
* **Interactive Primary Pressed Strong**: `--color-interactive-primary-pressed-strong`

---

## Shade & Intensity-Based Naming

### Intensity Scale

I support up to seven intensity steps:

1. weakest
2. weaker
3. weak
4. base (no suffix)
5. strong
6. stronger
7. strongest

There is no `-default` suffix.

Examples:

* **Background Surface Weak**: `--color-background-surface-weak`
* **Background Surface**: `--color-background-surface`
* **Text Strongest**: `--color-text-strongest`

### Shortened Scales

Not every role needs all seven steps. I allow shortened scales when:

* the role is rarely used
* additional steps are visually indistinguishable
* extra tokens would not be consumed by components

Consistency rules:

* the base token always exists
* I usually add only `-weakest` for backgrounds or `-strong` for contrast
* similar roles should follow the same pattern

Example:

* **Background Warning**: `--color-background-warning`
* **Background Warning Weakest**: `--color-background-warning-weakest`

---

## Layer 1: Primitives

Primitives are stable and value-oriented. They never express UI meaning.

### Color Primitives

I use numeric scales from 50 to 950.

Recommended naming:

* Neutral: `--neutral-50` … `--neutral-950`
* Brand: `--brand-50` … `--brand-950`
* Tailwind palettes: `--blue-50` … `--blue-950`, `--emerald-50` … `--emerald-950`

Examples:

* **Neutral 50**: `--neutral-50`
* **Neutral 900**: `--neutral-900`
* **Brand 600**: `--brand-600`
* **Blue 500**: `--blue-500`
* **Emerald 600**: `--emerald-600`
* **Red 600**: `--red-600`
* **Amber 500**: `--amber-500`

Rule:

* semantic tokens never contain raw values

### Radius Primitives

I use compact scale-based naming:

* `--radius01`
* `--radius04`
* `--radius08`
* `--radius12`

Examples:

* **Radius 01**: `--radius01`
* **Radius 04**: `--radius04`
* **Radius 08**: `--radius08`

#### Focus Radius

For every radius, I define a focus variant that is +2px.

Examples:

* **Radius 04 Focus**: `--radius04-focus`
* **Radius 08 Focus**: `--radius08-focus`

I use focus radius whenever a focus ring sits outside the element.

### Spacing Primitives

Naming:

* `--space0`, `--space100`, … `--space1000`

Rule:

* Space 100 equals 8px
* px = (token / 100) * 8

Examples:

* **Space 0**: `--space0`
* **Space 100**: `--space100` (8px)
* **Space 200**: `--space200` (16px)
* **Space 300**: `--space300` (24px)
* **Space 600**: `--space600` (48px)
* **Space 1000**: `--space1000` (80px)

### Border Width Primitives

Examples:

* **Border Width 1**: `--border-width-1`
* **Border Width 2**: `--border-width-2`

---

## Layer 2: Semantic Tokens

Semantic tokens express UI intent and intensity. Components only use this layer.

### Naming Structure

Developer structure:
`--<category>-<role>-(optional variant)-(optional state)-(optional intensity)`

Required categories:

* `--color-background-*`
* `--color-text-*`
* `--color-border-*`
* `--color-icon-*`

Recommended:

* `--color-interactive-*` for clickable elements

Utility:

* `--shadow-*` for structured shadows

---

## Semantic Roles and Examples

### Background

* **Background Primary**: `--color-background-primary`
* **Background Secondary**: `--color-background-secondary`
* **Background Surface**: `--color-background-surface`
* **Background Warning**: `--color-background-warning`
* **Background Success**: `--color-background-success`
* **Background Danger**: `--color-background-danger`

### Text

* **Text Default**: `--color-text-default`
* **Text Muted**: `--color-text-muted`
* **Text Inverse**: `--color-text-inverse`
* **Text Link**: `--color-text-link`

### Border

* **Border Default**: `--color-border-default`
* **Border Subtle**: `--color-border-subtle`
* **Border Strong**: `--color-border-strong`

### Icon

* **Icon Default**: `--color-icon-default`
* **Icon Muted**: `--color-icon-muted`
* **Icon Inverse**: `--color-icon-inverse`

---

## Interaction States

All states are supported:
hover, active, pressed, selected, disabled, focus, visited.

State to intensity mapping:

* hover -> `-hover-weakest`
* active -> `-active-weak`
* pressed -> `-pressed-strong`
* selected -> `-selected-stronger`
* disabled -> `-disabled-weaker`
* visited -> `-visited-strong`
* focus -> handled by focus tokens

Example:

* **Interactive Primary**: `--color-interactive-primary`
* **Interactive Primary Hover Weakest**: `--color-interactive-primary-hover-weakest`
* **Interactive Primary Active Weak**: `--color-interactive-primary-active-weak`
* **Interactive Primary Pressed Strong**: `--color-interactive-primary-pressed-strong`
* **Interactive Primary Selected Stronger**: `--color-interactive-primary-selected-stronger`
* **Interactive Primary Disabled Weaker**: `--color-interactive-primary-disabled-weaker`

---

## Focus Tokens (Outline-Based)

I handle focus with dedicated tokens.

Focus token set:

* **Focus Border Shadow**: `--shadow-focus-border`
* **Focus Border Color**: `--color-focus-border`
* **Focus Border Width**: `--border-width-focus`
* **Radius 04 Focus**: `--radius04-focus`

I combine them to draw a visible focus outline without layout shifts.

---

## Data Visualization Tokens

Data tokens represent chart series, not UI hierarchy.

### Categorical Series

I define eight series:

* **Data 1**: `--color-data-1`
* **Data 2**: `--color-data-2`
* **Data 3**: `--color-data-3`
* **Data 4**: `--color-data-4`
* **Data 5**: `--color-data-5`
* **Data 6**: `--color-data-6`
* **Data 7**: `--color-data-7`
* **Data 8**: `--color-data-8`

### States

* **Data 1 Hover Weakest**: `--color-data-1-hover-weakest`
* **Data 1 Selected Strong**: `--color-data-1-selected-strong`
* **Data 1 Muted Weaker**: `--color-data-1-muted-weaker`

Accessibility:

* I never rely on color alone
* I ensure contrast against chart backgrounds
* I recommend patterns or markers when needed

---

## Theming and Scalability

Semantic tokens enable theme switching.

Example:

* **Background Surface**: `--color-background-surface`

  * Light mode maps to `--neutral-50`
  * Dark mode maps to `--neutral-900`

Rules:

* I never rename existing tokens
* I add new tokens when needed
* I deprecate slowly and document changes

---

## Accessibility

Contrast rules:

* Text vs background meets WCAG requirements
* Icons and borders remain perceivable

Focus checklist:

* Focus ring visible on all surfaces
* Focus does not rely on color alone
* Focus uses dedicated tokens

Testing checklist:

* All states tested
* Light and dark mode tested
* Keyboard navigation tested
* Charts tested for color blindness

---

## Best Practices

* I never use raw values in components
* I always go through semantic tokens
* I keep naming order consistent
* I avoid unnecessary roles
* I shorten scales intentionally
* I treat focus as a system, not a state
* I document every new token
* I prefer meaning over appearance
* I keep primitives stable
* I keep semantics expressive
* I test before adding tokens
* I review tokens regularly

---

## Next Steps

1. Create two token sets in Figma Tokens:

   * Primitives
   * Semantic

2. Alias semantic tokens to primitives

3. Create theme variants by remapping semantic tokens

4. Export as CSS variables

5. Validate naming, ordering, and completeness

This file is the final reference for implementing and maintaining the design token system.
