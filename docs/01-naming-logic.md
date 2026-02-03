---

### 2. Plik: `docs/01-naming-logic.md`

```markdown
# Naming Logic & Scales

## 1. Designer vs. Developer Mapping
To bridge the gap between Figma and Code, I enforce a strict translation rule. We use two parallel names for every single token.

* **Designer Name:** Title Case, Spaces, Human-readable. (No `default` suffix).
* **CSS Variable:** Kebab-case, double-dash prefix, lowercase.

**The Mapping Rule:**
> Spaces become hyphens. Uppercase becomes lowercase.

### Examples
| Designer Name | CSS Variable |
| :--- | :--- |
| Background Weak | `--color-background-weak` |
| Text Strongest | `--color-text-strongest` |
| Border Danger Weak | `--color-border-danger-weak` |
| Shadow Focus Border | `--shadow-focus-border` |

## 2. Intensity Scale
I use a 7-step scale to describe visual weight.

1.  `weakest` (Subtle backgrounds)
2.  `weaker`
3.  `weak`
4.  **(Base)** (No suffix—this is the standard value)
5.  `strong`
6.  `stronger`
7.  `strongest` (High contrast text)

### Shortened Scales
Not every role requires all 7 steps.
* **Full Scale:** Used for Neutrals (Backgrounds/Text).
* **Short Scale:** Used for Status (Danger/Warning). I typically only define `Weakest` (for backgrounds), `Base` (for the solid color), and `Strong` (for text).

**Why no "-default" suffix?**
I treat the base token as the standard. `--color-background` is cleaner than `--color-background-default`. It implies it is the fallback.
