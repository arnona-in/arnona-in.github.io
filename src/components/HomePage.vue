<script setup>
import CustomerFeedback from './CustomerFeedback.vue'
defineEmits(['navigate'])
</script>
<template>
  <div>
    <section class="hero">
      <div class="hero-copy">
        <p class="eyebrow">The Onda collection · 2024</p>
        <h1>Carry a little<br /><em>calm.</em></h1>
        <p class="hero-intro">Beautifully made bottles for the rituals that make up your day. Thoughtful form, considered materials, and a quieter kind of utility.</p>
        <button class="primary-btn" @click="$emit('navigate', 'gallery')">Explore the collection <span>↗</span></button>
      </div>
      <div class="hero-art">
        <div class="sun"></div>
        <div class="arch"></div>
        <div class="bottle"><div class="bottle-cap"></div><div class="bottle-label">ONDA<small>hydrate slowly</small></div></div>
        <span class="art-note note-one">01 — Everyday<br />essentials</span>
        <span class="art-note note-two">Pure form.<br />Less noise.</span>
      </div>
    </section>
    <section class="intro-strip"><span>01</span><p>Designed in Melbourne<br />Made for everywhere</p><span class="strip-line"></span><p>Reusable by design<br />Loved for longer</p></section>
    <CustomerFeedback />
    <section class="home-cta"><p class="eyebrow">A better daily ritual</p><h2>Good things,<br /><em>well held.</em></h2><button class="outline-btn" @click="$emit('navigate', 'about')">Discover our story <span>↗</span></button></section>
  </div>
</template>
<style scoped>
.hero { max-width: 1200px; margin: auto; padding: 64px 30px 90px; display: grid; grid-template-columns: .87fr 1.13fr; gap: 60px; align-items: center; }
.hero-copy { padding-left: 7%; }
.eyebrow { color: var(--terracotta); text-transform: uppercase; font-size: 10px; letter-spacing: .18em; font-weight: 600; }
h1, h2 { font: 600 clamp(60px, 7vw, 100px)/.95 'Playfair Display', serif; letter-spacing: -.055em; margin: 24px 0 28px; }
em { color: var(--terracotta); font-style: italic; }
.hero-intro { color: var(--muted); max-width: 355px; font-size: 15px; line-height: 1.8; }
.primary-btn, .outline-btn { margin-top: 34px; border: 0; background: var(--ink); color: white; border-radius: 30px; padding: 15px 19px; font-size: 12px; transition: transform .2s, background .2s; }
.primary-btn:hover, .outline-btn:hover { transform: translateY(-2px); background: var(--terracotta); }
.primary-btn span, .outline-btn span { margin-left: 19px; }
.hero-art { min-height: 480px; background: #d9e1d1; position: relative; overflow: hidden; display: grid; place-items: center; }
.sun { position: absolute; width: 315px; height: 315px; border-radius: 50%; background: #e8b57d; top: 70px; left: 15%; }
.arch { position: absolute; width: 260px; height: 390px; border: 1px solid rgba(21,35,31,.2); border-bottom: 0; border-radius: 160px 160px 0 0; right: 16%; bottom: 0; }
.bottle { position: relative; width: 145px; height: 320px; border-radius: 42px 42px 30px 30px; background: linear-gradient(100deg, #bb6d47, #d7885b 52%, #b8603f); box-shadow: 22px 28px 30px rgba(54,61,45,.18); transform: rotate(6deg); }
.bottle-cap { position: absolute; width: 58px; height: 43px; left: 43px; top: -35px; border-radius: 9px 9px 3px 3px; background: #bea476; }
.bottle-label { position: absolute; top: 117px; left: 18px; right: 18px; padding: 16px 3px; text-align: center; border-top: 1px solid rgba(255,255,255,.4); border-bottom: 1px solid rgba(255,255,255,.4); color: #ffe4cf; font: 600 22px 'Playfair Display', serif; letter-spacing: .1em; }
.bottle-label small { display: block; margin-top: 7px; font: 7px 'DM Sans', sans-serif; letter-spacing: .16em; }
.art-note { position: absolute; font-size: 10px; line-height: 1.5; color: var(--ink); text-transform: uppercase; letter-spacing: .1em; }
.note-one { left: 24px; top: 25px; }.note-two { right: 28px; bottom: 24px; text-align: right; }
.intro-strip { max-width: 1040px; margin: auto; padding: 28px 30px; border-top: 1px solid var(--line); border-bottom: 1px solid var(--line); display: flex; gap: 42px; align-items: center; color: var(--muted); font-size: 12px; line-height: 1.65; }
.intro-strip > span:first-child { color: var(--terracotta); font-size: 10px; }.strip-line { flex: 1; border-top: 1px solid var(--line); }
.home-cta { max-width: 1040px; margin: 100px auto 20px; padding: 65px; background: var(--cream); text-align: center; }.home-cta h2 { font-size: clamp(48px, 6vw, 76px); }
.outline-btn { color: var(--ink); background: transparent; border: 1px solid var(--ink); margin-top: 0; }
@media (max-width: 700px) { .hero { padding: 38px 20px 60px; display: block; }.hero-copy { padding: 0; }.hero-intro { max-width: 320px; }.hero-art { min-height: 390px; margin-top: 65px; }.sun { width: 240px; height: 240px; }.bottle { transform: scale(.82) rotate(6deg); }.intro-strip { margin: 0 20px; gap: 18px; }.intro-strip .strip-line { display: none; }.home-cta { margin: 65px 20px 0; padding: 55px 20px; } }
</style>
