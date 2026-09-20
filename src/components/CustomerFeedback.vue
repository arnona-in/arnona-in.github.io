<template>
  <section class="feedback"><div class="feedback-head"><p class="eyebrow">Notes from the community</p><h2>A bottle worth<br /><em>talking about.</em></h2><span>✦</span></div><div class="feedback-grid"><blockquote v-for="quote in quotes" :key="quote.name">“{{ quote.text }}”<footer>— {{ quote.name }}</footer></blockquote></div></section>
</template>
<script setup>
const quotes = [{ text: 'It feels like a small luxury every time I pick it up. The best kind of everyday object.', name: 'Maya R.' }, { text: 'Finally, a bottle that looks at home on my desk and actually keeps my water cold.', name: 'Alex T.' }, { text: 'The Onda team made our studio order feel personal from the first email to the last delivery.', name: 'Lena K.' }]
</script>
<style scoped>
.feedback { max-width: 1040px; margin: 100px auto 0; padding: 0 30px; }.feedback-head { display: grid; grid-template-columns: 1fr 1fr auto; align-items: end; border-bottom: 1px solid var(--line); padding-bottom: 27px; }.feedback-head h2 { font: 500 41px/.98 'Playfair Display', serif; letter-spacing: -.04em; margin: 0; }.feedback-head > span { color: var(--terracotta); font-size: 28px; padding-bottom: 6px; }.feedback-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 22px; }.feedback blockquote { padding-top: 23px; color: var(--muted); font: 15px/1.7 'Playfair Display', serif; }.feedback blockquote footer { margin-top: 25px; color: var(--ink); font: 11px 'DM Sans', sans-serif; }@media (max-width: 700px) { .feedback { margin-top: 70px; padding: 0 20px; }.feedback-head { grid-template-columns: 1fr auto; gap: 20px; }.feedback-head .eyebrow { grid-column: span 2; }.feedback-head h2 { font-size: 35px; }.feedback-grid { grid-template-columns: 1fr; gap: 28px; } }
</style>
