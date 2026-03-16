<template>
  <nav :class="['navbar', { scrolled: isScrolled, 'menu-open': menuOpen }]">
    <div class="nav-inner">
      <a href="#" class="nav-logo" @mouseenter="onHover" @mouseleave="offHover">
        <span class="logo-icon">
          <svg width="32" height="32" viewBox="0 0 32 32" fill="none">
            <path d="M16 2L4 10V28H28V10L16 2Z" stroke="currentColor" stroke-width="1.5" fill="none"/>
            <path d="M10 28V18H22V28" stroke="currentColor" stroke-width="1.5"/>
            <path d="M16 10L10 14V20H22V14L16 10Z" fill="currentColor" opacity="0.3"/>
          </svg>
        </span>
        <span class="logo-text">Cedar<em>Africa</em></span>
      </a>

      <ul class="nav-links">
        <li v-for="link in links" :key="link.id">
          <a :href="'#' + link.id" @mouseenter="onHover" @mouseleave="offHover" @click="closeMenu">
            {{ link.label }}
          </a>
        </li>
      </ul>

      <a href="#booking" class="nav-cta" @mouseenter="onHover" @mouseleave="offHover" @click="closeMenu">
        Book a Call
      </a>

      <button class="hamburger" @click="menuOpen = !menuOpen" @mouseenter="onHover" @mouseleave="offHover">
        <span></span><span></span><span></span>
      </button>
    </div>

    <div class="mobile-menu">
      <ul>
        <li v-for="link in links" :key="link.id">
          <a :href="'#' + link.id" @click="closeMenu">{{ link.label }}</a>
        </li>
        <li><a href="#booking" class="mobile-cta" @click="closeMenu">Book a Call</a></li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const menuOpen = ref(false)

const links = [
  { id: 'about', label: 'About' },
  { id: 'services', label: 'Services' },
  { id: 'process', label: 'Process' },
  { id: 'testimonials', label: 'Stories' },
]

const emit = defineEmits(['hover', 'unhover'])
const onHover = () => emit('hover')
const offHover = () => emit('unhover')
const closeMenu = () => { menuOpen.value = false }

const handleScroll = () => { isScrolled.value = window.scrollY > 60 }
onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 1000;
  padding: 24px 0;
  transition: padding 0.4s var(--ease-out-expo), background 0.4s;
}
.navbar.scrolled {
  background: rgba(247,242,232,0.92);
  backdrop-filter: blur(20px);
  padding: 14px 0;
  border-bottom: 1px solid rgba(201,168,76,0.15);
}
.nav-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 40px;
  display: flex;
  align-items: center;
  gap: 40px;
}
.nav-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
  color: var(--forest);
  flex-shrink: 0;
}
.logo-icon { display: flex; color: var(--gold); }
.logo-text {
  font-family: var(--font-ui);
  font-size: 1.1rem;
  font-weight: 700;
  letter-spacing: 0.02em;
  color: var(--forest);
}
.logo-text em {
  font-style: normal;
  color: var(--gold);
}
.nav-links {
  display: flex;
  gap: 36px;
  list-style: none;
  margin-left: auto;
}
.nav-links a {
  font-family: var(--font-ui);
  font-size: 0.8rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  text-decoration: none;
  color: var(--forest);
  position: relative;
  padding-bottom: 2px;
}
.nav-links a::after {
  content: '';
  position: absolute;
  bottom: -2px; left: 0;
  width: 0; height: 1px;
  background: var(--gold);
  transition: width 0.3s var(--ease-out-expo);
}
.nav-links a:hover::after { width: 100%; }
.nav-cta {
  font-family: var(--font-ui);
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  text-decoration: none;
  color: var(--white);
  background: var(--forest);
  padding: 12px 24px;
  border: 1px solid var(--forest);
  transition: background 0.3s, color 0.3s, border-color 0.3s;
  white-space: nowrap;
}
.nav-cta:hover {
  background: var(--gold);
  border-color: var(--gold);
  color: var(--forest);
}
.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  padding: 4px;
  margin-left: auto;
}
.hamburger span {
  display: block;
  width: 24px;
  height: 1.5px;
  background: var(--forest);
  transition: all 0.3s;
}
.menu-open .hamburger span:nth-child(1) { transform: rotate(45deg) translate(5px, 5px); }
.menu-open .hamburger span:nth-child(2) { opacity: 0; }
.menu-open .hamburger span:nth-child(3) { transform: rotate(-45deg) translate(5px, -5px); }

.mobile-menu {
  display: none;
  background: var(--cream);
  padding: 0 40px;
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.4s var(--ease-out-expo), padding 0.4s;
}
.menu-open .mobile-menu {
  max-height: 400px;
  padding: 20px 40px 32px;
}
.mobile-menu ul { list-style: none; display: flex; flex-direction: column; gap: 20px; }
.mobile-menu a {
  font-family: var(--font-ui);
  font-size: 1.1rem;
  font-weight: 600;
  text-decoration: none;
  color: var(--forest);
  letter-spacing: 0.05em;
}
.mobile-cta {
  color: var(--gold) !important;
}

@media (max-width: 900px) {
  .nav-links, .nav-cta { display: none; }
  .hamburger { display: flex; }
  .mobile-menu { display: block; }
}
@media (max-width: 600px) {
  .nav-inner { padding: 0 20px; }
}
</style>
