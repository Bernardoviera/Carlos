---
name: ui-ux-pro-max
description: "UI/UX design intelligence. Search styles, palettes, typography, charts, UX guidelines. Actions: search, design system, style guide. Domains: style, color, typography, chart, landing, product, ux, google-fonts, icons. Stacks: html-tailwind, react, nextjs, vue, svelte, astro, swiftui, react-native, flutter, shadcn, nuxtjs, jetpack-compose."
argument-hint: "<query> [--domain style|color|typography|chart|landing|product|ux] [--stack html-tailwind|react|...]"
metadata:
  author: nextlevelbuilder
  version: "2.5.0"
---

# UI/UX Pro Max

Design intelligence skill powered by BM25 search over databases of 67 styles, 161 palettes, 57 font pairings, 25 chart types, and UX guidelines.

## Usage

```bash
# Domain search
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --domain <domain>

# Stack guidelines
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --stack <stack>

# Generate full design system
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --design-system -p "Project Name"

# Save design system to file
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --design-system --persist -p "Project Name"
```

## Domains
- `style` — UI styles (glassmorphism, minimalism, brutalism, dark mode, etc.)
- `color` — Color palettes by product type
- `typography` — Font pairings with Google Fonts imports
- `chart` — Chart types and library recommendations
- `landing` — Page structure and CTA strategies
- `product` — Product type recommendations (SaaS, e-commerce, portfolio)
- `ux` — Best practices and anti-patterns
- `google-fonts` — Google Fonts database
- `icons` — Icon library recommendations

## Stacks
`html-tailwind`, `react`, `nextjs`, `vue`, `svelte`, `astro`, `swiftui`, `react-native`, `flutter`, `shadcn`, `nuxtjs`, `nuxt-ui`, `jetpack-compose`, `threejs`, `angular`, `laravel`

## When Activated

When the user asks for design help, style recommendations, color palettes, typography, or UX guidelines:

1. Run the search command with the relevant query and domain
2. Present the top results clearly
3. Apply findings to the current project context

Auto-detect domain when `--domain` is omitted.
