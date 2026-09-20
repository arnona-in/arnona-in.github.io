<script setup>
import { computed, ref } from 'vue'

const today = new Date()
const requestedDay = Number(new URLSearchParams(window.location.search).get('date'))
const hasPreviewDay = Number.isInteger(requestedDay) && requestedDay >= 21 && requestedDay <= 26
const day = hasPreviewDay ? requestedDay : today.getDate()
const dateKey = hasPreviewDay ? 20260900 + day : today.getFullYear() * 10000 + (today.getMonth() + 1) * 100 + day
const birthdayKey = 20260926
const startKey = 20260921

const isBeforeReveal = computed(() => dateKey < startKey)
const isBirthday = computed(() => dateKey >= birthdayKey)
const explored = ref(false)
const confetti = ref([])

const dailyLines = {
  21: 'Umang, your kindness makes ordinary moments feel like little celebrations.',
  22: 'Umang, you carry a rare light — warm, brave, and wonderfully your own.',
  23: 'Umang, the world feels a little more hopeful wherever your thoughtful heart goes.',
  24: 'Umang, may your dreams find you ready, and may you always remember how loved you are.',
  25: 'Umang, you are becoming someone truly remarkable — keep choosing the beautiful path ahead.'
}

const dailyLine = computed(() => dailyLines[day] || dailyLines[25])
const ordinal = (value) => {
  const suffix = value % 10 === 1 && value % 100 !== 11 ? 'st' : value % 10 === 2 && value % 100 !== 12 ? 'nd' : value % 10 === 3 && value % 100 !== 13 ? 'rd' : 'th'
  return `${value}${suffix}`
}
const nextLabel = computed(() => day === 21 ? 'Check tomorrow' : `Wait till ${ordinal(day + 1)} September — check tomorrow`)

const playTone = (frequency, duration, offset = 0) => {
  const AudioContext = window.AudioContext || window.webkitAudioContext
  if (!AudioContext) return
  const context = new AudioContext()
  const oscillator = context.createOscillator()
  const gain = context.createGain()
  oscillator.type = 'sine'
  oscillator.frequency.value = frequency
  gain.gain.setValueAtTime(0.0001, context.currentTime + offset)
  gain.gain.exponentialRampToValueAtTime(0.13, context.currentTime + offset + 0.02)
  gain.gain.exponentialRampToValueAtTime(0.0001, context.currentTime + offset + duration)
  oscillator.connect(gain).connect(context.destination)
  oscillator.start(context.currentTime + offset)
  oscillator.stop(context.currentTime + offset + duration + 0.03)
}
document.title = isBirthday.value ? 'Happy 26th birthday, Umang!' : `A little something for you — ${day} September 2026`

const celebrate = () => {
  explored.value = true
  confetti.value = Array.from({ length: 32 }, (_, index) => ({
    id: `${Date.now()}-${index}`,
    left: `${8 + Math.random() * 84}%`,
    delay: `${Math.random() * 0.35}s`,
    color: ['#d87862', '#edb866', '#7da69b', '#b985c4', '#f3d494'][index % 5],
    rotate: `${Math.round(Math.random() * 240)}deg`
  }))
  if (isBirthday.value) {
    ;[262, 262, 294, 262, 349, 330, 262, 262, 294, 262, 392, 349].forEach((note, index) => playTone(note, 0.28, index * 0.22))
  } else {
    playTone(523, 0.2)
    playTone(659, 0.25, 0.15)
  }
}
</script>

<template>
  <section class="for-you-page">
    <div class="for-you-orb orb-one"></div>
    <div class="for-you-orb orb-two"></div>
    <span v-for="piece in confetti" :key="piece.id" class="confetti" :style="{ left: piece.left, animationDelay: piece.delay, background: piece.color, transform: `rotate(${piece.rotate})` }"></span>

    <div class="for-you-card">
      <div v-if="isBeforeReveal" class="for-you-message">
        <div class="waiting-star">✦</div>
        <h1>Wait a little<br /><em>and check on 21st.</em></h1>
        <p>Your little pocket of joy is getting ready.</p>
      </div>
      <div v-else-if="isBirthday" class="for-you-message birthday-message">
        <div class="birthday-cake">✦</div>
        <p class="date-stamp">26 · 09 · 2026</p>
        <h1>Happy 26th<br /><em>birthday, Umang.</em></h1>
        <p class="poem">May every road you take be gentle,<br />may every dream find a door,<br />and may your beautiful heart<br />always know what it is here for.<br /><br />You are on a good path, Umang —<br />keep walking it with your bright, brave grace.<br />The world is luckier with you in it.</p>
        <button class="for-you-button" @click="celebrate">Open your birthday wish <span>✦</span></button>
        <p v-if="explored" class="after-message">Twenty-six in 2026 — a special little alignment, made just for you. 🎂</p>
      </div>
      <div v-else class="for-you-message">
        <p class="date-stamp">{{ day }} · 09 · 2026</p>
        <div class="daily-sparkle">✦</div>
        <h1>Today has<br /><em>something for you.</em></h1>
        <p v-if="!explored">A tiny pause. A kind thought. A whole day that belongs to you.</p>
        <!-- <p v-else class="revealed-line">{{ dailyLine }}</p> -->
        <button v-if="!explored" class="for-you-button" @click="celebrate">Explore your day <span>↗</span></button>
        <div v-else class="next-reveal"><p>{{ dailyLine }}</p><button class="for-you-button secondary" @click="playTone(392, 0.3)">{{ nextLabel }} <span>→</span></button></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.for-you-page { min-height: 700px; position: relative; display: grid; place-items: center; overflow: hidden; padding: 65px 20px 90px; background: #faeee7; }
.for-you-card { position: relative; z-index: 2; width: min(650px, 100%); min-height: 560px; padding: 58px 45px 34px; display: flex; flex-direction: column; justify-content: space-between; text-align: center; background: rgba(255, 252, 248, .86); border: 1px solid rgba(200, 119, 95, .25); box-shadow: 0 20px 70px rgba(160, 92, 75, .13); animation: card-in .8s ease both; }
.for-you-kicker, .date-stamp { color: #bb6b57; font-size: 10px; text-transform: uppercase; letter-spacing: .2em; font-weight: 600; }
.for-you-message { flex: 1; display: flex; flex-direction: column; justify-content: center; align-items: center; }
.for-you-message h1 { margin: 20px 0 20px; font: 600 clamp(46px, 7vw, 73px)/.96 'Playfair Display', serif; letter-spacing: -.06em; color: #29473e; }
.for-you-message em { color: #c76b45; }
.for-you-message > p:not(.date-stamp):not(.poem):not(.after-message) { max-width: 330px; color: #7d766f; font-size: 14px; line-height: 1.75; }
.waiting-star, .daily-sparkle, .birthday-cake { color: #e2a453; font-size: 43px; animation: float 3s ease-in-out infinite; }
.for-you-button { border: 0; border-radius: 40px; padding: 15px 22px; margin-top: 29px; color: #fffaf5; background: #29473e; font-size: 12px; transition: transform .2s, background .2s; }
.for-you-button:hover { transform: translateY(-3px); background: #c76b45; }.for-you-button span { margin-left: 18px; }
.next-reveal { animation: reveal .6s ease both; }.next-reveal > p, .revealed-line { max-width: 390px; color: #29473e; font: 500 22px/1.45 'Playfair Display', serif; }
.for-you-button.secondary { margin-top: 25px; color: #29473e; background: transparent; border: 1px solid #29473e; }.for-you-footer { color: #9e897e; font: 12px 'Playfair Display', serif; }.for-you-footer span { color: #d27762; font-size: 16px; margin-left: 4px; }
.poem { color: #625f59; font: 16px/1.75 'Playfair Display', serif; }.birthday-message h1 { margin-top: 14px; font-size: clamp(43px, 6vw, 65px); }.after-message { margin-top: 20px; color: #c76b45; font-size: 12px; }
.for-you-orb { position: absolute; border-radius: 50%; filter: blur(1px); opacity: .65; }.orb-one { width: 350px; height: 350px; top: -130px; left: -90px; background: #f2c7ba; }.orb-two { width: 420px; height: 420px; bottom: -210px; right: -140px; background: #d5e4ce; }.confetti { position: absolute; z-index: 4; top: -20px; width: 8px; height: 17px; animation: fall 2.2s ease-in forwards; }
@keyframes card-in { from { opacity: 0; transform: translateY(18px) scale(.98); } to { opacity: 1; transform: none; } } @keyframes float { 50% { transform: translateY(-8px) rotate(8deg); } } @keyframes reveal { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: none; } } @keyframes fall { to { top: 105%; transform: translateY(0) rotate(540deg); } }
@media (max-width: 600px) { .for-you-page { padding: 35px 16px 55px; min-height: 650px; }.for-you-card { min-height: 580px; padding: 40px 20px 28px; }.poem { font-size: 14px; }.next-reveal > p, .revealed-line { font-size: 19px; } }
</style>
