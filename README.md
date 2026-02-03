# Shade & Intensity Design System

Welcome to the documentation for our Token Architecture. This repository serves as the single source of truth for our design tokens, bridging the gap between design (Figma) and engineering (CSS).

## 🚀 Overview

We utilize a **Shade & Intensity-Based Naming** convention. We prioritize semantic meaning (what it does) and intensity (how strong it looks) over raw values.

### Core Philosophy
1.  **No Raw Values:** UI components never reference Hex codes or pixels directly.
2.  **Bilingual:** We support a strict mapping between "Designer English" and "Developer CSS."
3.  **Themable:** Intensity is relative. "Strong" means dark in Light Mode, but light in Dark Mode.

## 📐 Token Hierarchy

We organize the system into three distinct layers. Data flows strictly from left to right.

```ascii
[ Layer 1: Primitives ]      [ Layer 2: Semantic ]        [ Layer 3: Components ]
   Raw Values                   Context & Intent               Implementation
+---------------------+      +---------------------+      +---------------------+
|                     |      |                     |      |                     |
|  brand-500 (#3B82F6)| ---> |  Background Primary | ---> |  Button (Primary)   |
|  neutral-100        |      |                     |      |  Card               |
|  space-100 (8px)    |      |  Spacing Layout     |      |  Input Field        |
|                     |      |                     |      |                     |
+---------------------+      +---------------------+      +---------------------+
           ^                            ^                            ^
    (Stable / Global)           (Theme Dependent)           (Composition)
