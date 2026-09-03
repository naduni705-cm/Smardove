<script setup>
defineProps({
  color: { type: String, default: '#8b8f95' },
  fillId: { type: String, required: true }
})

const path =
  'M0,70 C15,55 25,60 40,45 C55,30 65,50 80,40 C95,30 110,42 125,30 C140,18 155,35 170,22 C185,9 200,20 215,8 C230,-4 245,15 260,0 C275,-14 290,5 300,-10'
</script>

<template>
  <svg viewBox="0 0 300 90" preserveAspectRatio="none">
    <defs>
      <linearGradient :id="fillId" x1="0" y1="0" x2="0" y2="1">
        <stop offset="0%" :stop-color="color" stop-opacity="0.25" />
        <stop offset="100%" :stop-color="color" stop-opacity="0" />
      </linearGradient>
    </defs>
    <g transform="translate(0,55)">
      <path :d="path + ' L300,90 L0,90 Z'" :fill="`url(#${fillId})`" />
      <path :d="path" fill="none" :stroke="color" stroke-width="2" stroke-linecap="round" />
      <circle cx="300" cy="-10" r="4.5" fill="#fff" :stroke="color" stroke-width="2" />
    </g>
  </svg>
</template>

<style scoped>
svg {
  display: block;
  width: 100%;
  height: auto;
}
</style>