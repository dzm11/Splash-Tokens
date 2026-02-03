# Design System Token Documentation: Shade & Intensity

This documentation defines the architecture and naming conventions for the design system tokens. It ensures a seamless handoff between design and engineering by establishing a unified language based on visual intensity and semantic intent.

## 📌 Table of Contents

* [1. Architecture Overview](https://www.google.com/search?q=%231-architecture-overview)
* [2. Naming Philosophy](https://www.google.com/search?q=%232-naming-philosophy)
* [3. Token Hierarchy](https://www.google.com/search?q=%233-token-hierarchy)
* [4. Designer & Developer Mapping](https://www.google.com/search?q=%234-designer--developer-mapping)
* [5. Primitive Layer](https://www.google.com/search?q=%235-primitive-layer)
* [6. Semantic Layer](https://www.google.com/search?q=%236-semantic-layer)
* [7. Focus & Accessibility System](https://www.google.com/search?q=%237-focus--accessibility-system)
* [8. Data Visualization](https://www.google.com/search?q=%238-data-visualization)
* [9. Theming & Scalability](https://www.google.com/search?q=%239-theming--scalability)
* [10. Token Catalog Examples](https://www.google.com/search?q=%2310-token-catalog-examples)
* [11. Best Practices](https://www.google.com/search?q=%2311-best-practices)
* [12. Implementation Guide](https://www.google.com/search?q=%2312-implementation-guide)

---

## 1. Architecture Overview

The system utilizes a **Shade & Intensity-Based** approach. Tokens are named according to their functional role and their relative visual weight (intensity) rather than static color values (e.g., "Blue 500"). This allows the system to remain theme-agnostic and scalable.

## 2. Naming Philosophy

By using intensity-based naming (Weakest to Strongest), the system achieves:

* **Theme Scalability:** A "Background Weak" token remains conceptually consistent whether the interface is in Light or Dark mode.
* **Predictability:** Designers and developers can anticipate the visual hierarchy based on the suffix.
* **Semantic Clarity:** Tokens describe the "why" and "how much" rather than the "what color."

## 3. Token Hierarchy

Data flows through a three-tier architecture to ensure maintainability:

```ascii
[ Layer 1: Primitives ]      [ Layer 2: Semantic ]        [ Layer 3: Components ]
   Raw Global Values            Context & Intent               Implementation
+---------------------+      +---------------------+      +---------------------+
|                     |      |                     |      |                     |
|  brand-500 (#3B82F6)| ---> |  Background Primary | ---> |  Button (Primary)   |
|  neutral-100        |      |                     |      |  Card               |
|  space-100 (8px)    |      |  Spacing Layout     |      |  Input Field        |
|                     |      |                     |      |                     |
+---------------------+      +---------------------+      +---------------------+

```

## 4. Designer & Developer Mapping

The system enforces two parallel naming layers. Every token must have both a human-readable name for designers and a technical variable for developers.

* **Designer-facing:** English, Title Case, no technical prefixes (e.g., `Text Strongest`).
* **Developer-facing:** Kebab-case CSS variables with a double-dash prefix (e.g., `--color-text-strongest`).

**Mapping Rule:** To derive the Designer Name from the CSS variable, remove the `--category-` prefix, replace hyphens with spaces, and apply Title Case.

---

## 5. Primitive Layer

Primitives are stable, global values. They are not UI-contextual and should never be used directly in component styles.

### Color Primitives

Standard palettes follow the 50–950 scale:

* **Neutral:** `neutral-50` to `neutral-950`
* **Brand:** `brand-50` to `brand-950`
* **Tailwind Palettes:** `blue-50`, `emerald-50`, `rose-50`, etc.

### Radius Primitives

Naming follows the format `radius[px]`:

* **Scale:** `radius04` (4px), `radius08` (8px), `radius12` (12px).
* **Focus Radius:** Every radius has a corresponding `*-focus` token (e.g., `radius04-focus`) calculated as `Base Radius + 2px`.

### Spacing Primitives

A linear scale where `100` units equals `8px` (the base unit):

* `space050` (4px), `space100` (8px), `space200` (16px), `space400` (32px).

### Border Width Primitives

* `Width 1` (`--border-width-1`): 1px for standard borders.
* `Width 2` (`--border-width-2`): 2px for focus and active states.

---

## 6. Semantic Layer

Semantic tokens map primitives to specific UI roles and intensities.

### Naming Structure

`--<category>-<role>-<optional-variant>-<optional-state>-<optional-intensity>`

### Intensity Scale

The system supports up to 7 steps of intensity:
`weakest` → `weaker` → `weak` → **(base)** → `strong` → `stronger` → `strongest`.

**Constraint:** The base token has no suffix (e.g., `--color-background`, not `--color-background-default`).

### Shortened Scales

Not all roles require 7 steps. Status-based roles (Warning, Danger, Success) typically use a reduced set:

* `weakest`: Used for subtle background fills (e.g., Alerts).
* `base`: Used for standard icons and solid button backgrounds.
* `strong`: Used for text labels to ensure contrast.

---

## 7. Focus & Accessibility System

Focus states are managed via an outline-based approach to prevent layout shifts.

* **Focus Shadow:** `--shadow-focus-border` (typically a 2px spread box-shadow).
* **Focus Color:** `--color-focus-border` defines the ring color.
* **Focus Radius:** Components must switch to the `radius-*-focus` token when focused to ensure the ring sits outside the element without clipping.

## 8. Data Visualization

Tokens for charts are derived from Tailwind primitives to ensure distinct categorical colors:

* **Series:** `--color-data-1` through `--color-data-8`.
* **States:** Includes `-hover` (increased intensity) and `-muted` (desaturated for unselected states).

---

## 9. Theming & Scalability

Semantic tokens enable theme switching by re-mapping to different primitives.

* **Theme Inversion:** In Dark Mode, `Background Weak` maps to a dark primitive (`neutral-900`), while in Light Mode, it maps to a light primitive (`neutral-50`).
* **Compatibility:** New intensity steps can be added without breaking existing component implementations.

---

## 10. Token Catalog Examples

### Primitive Examples

| Designer Name | CSS Variable | Value |
| --- | --- | --- |
| Brand 500 | `--color-brand-500` | #3B82F6 |
| Neutral 950 | `--color-neutral-950` | #171717 |
| Radius 08 | `--radius-08` | 8px |
| Radius 08 Focus | `--radius-08-focus` | 10px |
| Space 100 | `--space-100` | 8px |
| Width 2 | `--border-width-2` | 2px |

### Semantic Examples

| Designer Name | CSS Variable | Purpose |
| --- | --- | --- |
| Background Weak | `--color-background-weak` | Card or sidebar background |
| Text Strongest | `--color-text-strongest` | High-contrast headings |
| Border Subtle | `--color-border-subtle` | Dividers and separators |
| Icon Muted | `--color-icon-muted` | Decorative or disabled icons |
| Background Primary | `--color-background-primary` | Main CTA background |
| Background Primary Hover | `--color-background-primary-hover` | Button hover state |

### Common Mistakes & Corrected Versions

| Incorrect Variable | Corrected Variable | Reason |
| --- | --- | --- |
| `--color-text-default` | `--color-text` | "Default" suffix is prohibited. |
| `--color-red-500` | `--color-background-danger` | Variables must be semantic. |
| `--BackgroundPrimary` | `--color-background-primary` | Kebab-case is required. |
| `--text-2` | `--text-weak` | Intensity names are required over numbers. |

---

## 11. Best Practices

* **Suffix Exclusion:** Never use the `-default` suffix; the base token represents the standard value.
* **Aliasing Hierarchy:** Semantic tokens must alias Primitives. Raw values (hex/px) are prohibited in the Semantic layer.
* **Intensity Logic:** Every hover state should shift one step toward higher contrast (e.g., `base` to `strong`).
* **Focus Outline:** Use `box-shadow` or `outline` for focus rings; never modify `border-color` alone.
* **Contrast Compliance:** All `Text` and `Icon` tokens must be validated against their respective `Background` tokens for WCAG accessibility.
* **Semantic over Visual:** Select tokens based on their function in the interface, not their current color.

## 12. Implementation Guide

1. **Figma Setup:** Use the Tokens Studio plugin to define the "Primitive" and "Semantic" sets.
2. **Variable Transformation:** Utilize a tool like Style Dictionary to transform JSON tokens into CSS/SCSS variables.
3. **Theming:** Create separate files or blocks for Light and Dark modes, re-defining only the Semantic mappings.
4. **Handoff:** Ensure all design files use the "Designer Name" while the exported code uses the "CSS Variable."

---

*End of Documentation*

Would you like me to generate a sample JSON structure for these tokens to use in Figma Tokens or Style Dictionary?
