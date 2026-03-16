<template>
  <div id="app">
    <!-- Custom cursor -->
    <div class="cursor" :style="{ left: cursor.x + 'px', top: cursor.y + 'px' }" :class="{ hovering: isHovering }"></div>
    <div class="cursor-follower" :style="{ left: follower.x + 'px', top: follower.y + 'px' }" :class="{ hovering: isHovering }"></div>

    <!-- Page loader -->
    <div class="loader" :class="{ loaded: pageLoaded }">
      <div class="loader-inner">
        <svg width="40" height="40" viewBox="0 0 32 32" fill="none">
          <path d="M16 2L4 10V28H28V10L16 2Z" stroke="#C9A84C" stroke-width="1.5" fill="none"/>
          <path d="M10 28V18H22V28" stroke="#C9A84C" stroke-width="1.5"/>
        </svg>
        <div class="loader-bar"><div class="loader-progress" :style="{ width: loadProgress + '%' }"></div></div>
      </div>
    </div>

    <NavBar @hover="setHover(true)" @unhover="setHover(false)" />
    <HeroSection @hover="setHover(true)" @unhover="setHover(false)" />
    <AboutSection />
    <ServicesSection @hover="setHover(true)" @unhover="setHover(false)" />
    <ProcessSection @hover="setHover(true)" @unhover="setHover(false)" />
    <TestimonialsSection @hover="setHover(true)" @unhover="setHover(false)" />
    <BookingSection @hover="setHover(true)" @unhover="setHover(false)" />
    <FooterSection @hover="setHover(true)" @unhover="setHover(false)" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import ProcessSection from './components/ProcessSection.vue'
import TestimonialsSection from './components/TestimonialsSection.vue'
import BookingSection from './components/BookingSection.vue'
import FooterSection from './components/FooterSection.vue'

const cursor = ref({ x: -100, y: -100 })
const follower = ref({ x: -100, y: -100 })
const isHovering = ref(false)
const pageLoaded = ref(false)
const loadProgress = ref(0)

const setHover = (v) => { isHovering.value = v }

onMounted(() => {
  // Loader animation
  let prog = 0
  const interval = setInterval(() => {
    prog += Math.random() * 15
    loadProgress.value = Math.min(prog, 95)
    if (prog >= 95) {
      clearInterval(interval)
      setTimeout(() => {
        loadProgress.value = 100
        setTimeout(() => { pageLoaded.value = true }, 400)
      }, 300)
    }
  }, 80)

  // Smooth cursor
  let fx = -100, fy = -100
  window.addEventListener('mousemove', (e) => {
    cursor.value = { x: e.clientX, y: e.clientY }
    const lerp = (a, b, t) => a + (b - a) * t
    const animate = () => {
      fx = lerp(fx, e.clientX, 0.12)
      fy = lerp(fy, e.clientY, 0.12)
      follower.value = { x: fx, y: fy }
    }
    requestAnimationFrame(animate)
  })
})
</script>

<style>
/* Loader */
.loader {
  position: fixed;
  inset: 0;
  background: var(--forest-deep);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 99997;
  transition: opacity 0.6s var(--ease-out-expo), visibility 0.6s;
}
.loader.loaded {
  opacity: 0;
  visibility: hidden;
  pointer-events: none;
}
.loader-inner {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 24px;
}
.loader-inner svg {
  animation: pulse 1.5s ease-in-out infinite;
}
@keyframes pulse {
  0%, 100% { opacity: 0.6; transform: scale(0.95); }
  50% { opacity: 1; transform: scale(1.05); }
}
.loader-bar {
  width: 180px;
  height: 1px;
  background: rgba(247,242,232,0.1);
  overflow: hidden;
}
.loader-progress {
  height: 100%;
  background: var(--gold);
  transition: width 0.2s var(--ease-out-expo);
}
</style>
