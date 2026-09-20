<script setup>
import { ref } from 'vue'
import HomePage from './components/HomePage.vue'
import AboutPage from './components/AboutPage.vue'
import GalleryPage from './components/GalleryPage.vue'
import ContactPage from './components/ContactPage.vue'
import SocialLinks from './components/SocialLinks.vue'
import ForYouPage from './components/ForYouPage.vue'

const currentPage = ref(window.location.pathname === '/for-you' ? 'for-you' : 'home')
const menuOpen = ref(false)

const navigate = (page) => {
  currentPage.value = page
  menuOpen.value = false
  const path = page === 'for-you' ? '/for-you' : '/'
  window.history.pushState({}, '', path)
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <div class="app-shell">
    <!-- <header v-if="currentPage !== 'for-you'" class="site-header">
      <a class="brand" href="#" @click.prevent="navigate('home')">
        <span class="brand-mark">O</span>
        <span>Onda<small>BOTANICAL BOTTLES</small></span>
      </a>
      <button class="menu-toggle" aria-label="Toggle navigation" @click="menuOpen = !menuOpen">
        <span></span><span></span>
      </button>
      <nav class="main-nav" :class="{ 'is-open': menuOpen }" aria-label="Main navigation">
        <button :class="{ active: currentPage === 'home' }" @click="navigate('home')">Home</button>
        <button :class="{ active: currentPage === 'about' }" @click="navigate('about')">About</button>
        <button :class="{ active: currentPage === 'gallery' }" @click="navigate('gallery')">Gallery</button>
        <button class="nav-contact" @click="navigate('contact')">Contact us <span>↗</span></button>
      </nav>
    </header> -->

    <main>
      <Transition name="page" mode="out-in">
        <ForYouPage v-if="currentPage === 'for-you'" key="for-you" />
        <!-- <HomePage v-else-if="currentPage === 'home'" key="home" @navigate="navigate" />
        <AboutPage v-else-if="currentPage === 'about'" key="about" @navigate="navigate" />
        <GalleryPage v-else-if="currentPage === 'gallery'" key="gallery" @navigate="navigate" />
        <ContactPage v-else key="contact" /> -->
      </Transition>
    </main>

    <!-- <footer v-if="currentPage !== 'for-you'" class="site-footer">
      <div class="footer-top">
        <div class="footer-brand">
          <a class="brand" href="#" @click.prevent="navigate('home')">
            <span class="brand-mark">O</span><span>Onda<small>BOTANICAL BOTTLES</small></span>
          </a>
          <p>Thoughtful vessels for everyday rituals.</p>
        </div>
        <SocialLinks />
        <div class="footer-cta">
          <span>Start a conversation</span>
          <button @click="navigate('contact')">Let's talk <span>↗</span></button>
        </div>
      </div>
      <div class="footer-bottom"><span>© 2024 Onda Bottles. Crafted with intention.</span><span>Made for a slower way of living.</span></div>
    </footer> -->
  </div>
</template>
