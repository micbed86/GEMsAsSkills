---
name: knowledge-visualizer
description: Generates aesthetic, responsive, and interactive knowledge cards and dashboards in HTML and CSS, allowing for rapid structuring and assimilation of complex data.

---

# Knowledge Visualizer - Fact Sheet

This skill allows for the rapid transformation of raw data and complex concepts into memorable, interactive user interfaces (UI). The goal is to achieve maximum cognitive impact using minimalist, clean code.

## When to use this skill

- When the Master needs to clearly present a complex process, a set of statistics, or technical rules.

- When you want to create an interactive summary, dashboard, or a Bento Grid-style structure.

- When raw text is too monotonous or difficult to analyze quickly.

## How to use it

### 1. Styling and Design System (Dark Editorial Premium)

Implement a consistent, professional, and modern look:

- **Background:** Deep, saturated darkness (e.g., `#0D0F14`).

- **UI Elements:** Glassmorphism effect with background blur (`backdrop-filter: blur()`) and subtle, translucent borders.

- **Rounding:** Modern edge rounding (standard Tailwind classes like `rounded-2xl` or `rounded-3xl`).

- **Whitespace:** Plenty of clear space to allow for breathing room and easy visual scanning.

- **Typography:** Clean, modern sans-serif fonts (standard Inter from Google Fonts).

### 2. Information Architecture and Interaction

- **Bento Grid Layout:** Divide information into tiles of varying sizes and visual weights. The most important statistics or main principles should occupy the largest blocks.

- **Interactivity:** Add simple, flawless interactive mechanisms (e.g., filters, tabbed cards, accordions, calculators) written in vanilla JavaScript.

- **Responsiveness (RWD):** The code must look impeccable on both desktop monitors and mobile phone screens. Avoid rigid widths in pixels.

### 3. Technical Standards and Security

- **No external JS libraries:** Avoid loading unnecessary, heavy scripts.

- **CSS Packages:** If using Tailwind, load it only from a secure CDN in the head section.

- **CSP (Content Security Policy) Protection:** To prevent the interface from breaking in environments with restrictive CSP, always include a basic `<style>` block containing critical styles (layout, background, and text colors) as a fallback.

- **SVG Attributes:** Always define `width` and `height` parameters directly in the `<svg>` tag for every SVG element. This prevents them from appearing oversized before the CSS sheet loads.

### 4. Content Discipline

- Never simplify or remove substantive information for the sake of appearance.

- The code must be complete, fully functional, and without placeholder comments.
