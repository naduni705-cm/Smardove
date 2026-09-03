# Hero Vue Project

A Vite + Vue 3 project recreating the "Boost Your Revenue with Tailored Financial Tools" hero
section, built with `vw` / `vh` / `clamp()` fluid units so it scales smoothly across screen sizes.

## Structure

```
hero-vue-project/
├── index.html            Vite entry HTML
├── package.json
├── vite.config.js
├── src/
│   ├── main.js            App bootstrap
│   ├── style.css          Global reset
│   ├── App.vue            Root component
│   └── components/
│       ├── Hero.vue       Hero section (headline, CTAs, dashboard mock)
│       └── ChartSVG.vue   Reusable line-chart SVG component
```

## Setup

```bash
npm install
npm run dev
```

Then open the local URL Vite prints (usually http://localhost:5173).

## Build

```bash
npm run build
npm run preview
```

## Notes

- All spacing, font sizes, and layout widths use `vw`/`vh`/`clamp()` instead of fixed `px`
  breakpoints, so the design scales fluidly with viewport size.
- A single `max-width: 700px` media query handles the switch to a stacked mobile layout,
  since pure viewport units alone don't hold up well below phone widths.
- Account and transaction data live in `Hero.vue`'s `<script setup>` as reactive arrays —
  edit those to change the numbers shown.
