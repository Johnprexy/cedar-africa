<template>
  <section class="services" id="services">
    <div class="services-inner">
      <div class="services-header">
        <span class="section-label reveal">What We Do</span>
        <h2 class="services-title reveal reveal-delay-1">
          End-to-end property<br/><em>solutions</em> for the diaspora.
        </h2>
        <p class="services-sub reveal reveal-delay-2">
          From finding the perfect plot to handing you the keys — we handle every step, every update, every decision. You stay in the loop from wherever you are in the world.
        </p>
      </div>

      <div class="services-grid">
        <div
          class="service-card reveal"
          :class="'reveal-delay-' + (i + 1)"
          v-for="(s, i) in services"
          :key="s.title"
          @mouseenter="hovered = i; $emit('hover')"
          @mouseleave="hovered = null; $emit('unhover')"
          :style="{ '--accent': s.color }"
        >
          <div class="card-number">0{{ i + 1 }}</div>
          <div class="card-icon">{{ s.icon }}</div>
          <h3 class="card-title">{{ s.title }}</h3>
          <p class="card-desc">{{ s.desc }}</p>
          <ul class="card-features">
            <li v-for="f in s.features" :key="f">{{ f }}</li>
          </ul>
          <div class="card-arrow">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
              <path d="M4 10H16M10 4L16 10L10 16" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            </svg>
          </div>
          <div class="card-glow"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
defineEmits(['hover', 'unhover'])
const hovered = ref(null)

const services = [
  {
    icon: '🏗', title: 'Land Acquisition', color: '#C9A84C',
    desc: 'We identify, verify, and acquire land on your behalf — with full title checks and legal clearance.',
    features: ['Title verification', 'Government survey', 'Legal documentation', 'Secure escrow payments'],
  },
  {
    icon: '📐', title: 'Design & Architecture', color: '#2A5040',
    desc: 'Our architects bring your vision to life with 3D renders and detailed structural plans before breaking ground.',
    features: ['3D visualizations', 'Architectural drawings', 'Material selection', 'Cost estimation'],
  },
  {
    icon: '🏛', title: 'Construction Management', color: '#C9A84C',
    desc: 'Vetted contractors, supervised timelines, and rigorous quality control at every stage of construction.',
    features: ['Site supervision', 'Weekly updates', 'Quality assurance', 'Timeline management'],
  },
  {
    icon: '📷', title: 'Progress Reporting', color: '#2A5040',
    desc: 'Stay connected to your project from anywhere. Monthly video reports, live site feeds, and a dedicated dashboard.',
    features: ['Monthly video updates', 'Photo documentation', 'Client dashboard', 'WhatsApp briefings'],
  },
  {
    icon: '🔑', title: 'Property Management', color: '#C9A84C',
    desc: 'Once built, we manage your property — finding tenants, collecting rent, and maintaining the asset.',
    features: ['Tenant screening', 'Rent collection', 'Maintenance handling', 'Financial reporting'],
  },
  {
    icon: '⚖️', title: 'Legal & Compliance', color: '#2A5040',
    desc: 'Navigate Nigerian property law with ease. Our legal team handles every regulatory and documentation requirement.',
    features: ['C of O processing', 'Deed of Assignment', 'Survey plans', 'Tax compliance'],
  },
]

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible') })
  }, { threshold: 0.1 })
  document.querySelectorAll('.services .reveal').forEach(el => observer.observe(el))
})
</script>

<style scoped>
.services {
  padding: 120px 80px;
  background: var(--forest-deep);
  position: relative;
  overflow: hidden;
}
.services::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: radial-gradient(circle at 20% 80%, rgba(201,168,76,0.06) 0%, transparent 50%),
                    radial-gradient(circle at 80% 20%, rgba(42,80,64,0.2) 0%, transparent 50%);
  pointer-events: none;
}
.services-inner { max-width: 1200px; margin: 0 auto; }
.services-header {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: start;
  gap: 40px;
  margin-bottom: 72px;
}
.services-title {
  font-family: var(--font-display);
  font-size: clamp(2rem, 3.5vw, 3.2rem);
  font-weight: 300;
  line-height: 1.2;
  color: var(--cream);
}
.services-title em { font-style: italic; color: var(--gold); }
.services-sub {
  font-size: 0.95rem;
  line-height: 1.75;
  color: rgba(247,242,232,0.55);
  max-width: 360px;
}
.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2px;
}
.service-card {
  position: relative;
  background: rgba(247,242,232,0.03);
  border: 1px solid rgba(247,242,232,0.06);
  padding: 40px 36px;
  overflow: hidden;
  transition: background 0.4s, transform 0.4s var(--spring), border-color 0.4s;
  cursor: pointer;
}
.service-card:hover {
  background: rgba(247,242,232,0.06);
  border-color: var(--accent);
  transform: translateY(-4px);
}
.card-number {
  position: absolute;
  top: 30px; right: 30px;
  font-family: var(--font-display);
  font-size: 3rem;
  font-weight: 700;
  color: rgba(247,242,232,0.05);
  line-height: 1;
}
.card-icon { font-size: 2rem; margin-bottom: 24px; }
.card-title {
  font-family: var(--font-ui);
  font-size: 1rem;
  font-weight: 700;
  color: var(--cream);
  margin-bottom: 12px;
  letter-spacing: 0.02em;
}
.card-desc {
  font-size: 0.88rem;
  line-height: 1.7;
  color: rgba(247,242,232,0.5);
  margin-bottom: 20px;
}
.card-features {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.card-features li {
  font-size: 0.8rem;
  color: rgba(247,242,232,0.35);
  padding-left: 14px;
  position: relative;
}
.card-features li::before {
  content: '';
  position: absolute;
  left: 0; top: 50%;
  width: 6px; height: 1px;
  background: var(--accent);
  transform: translateY(-50%);
}
.card-arrow {
  position: absolute;
  bottom: 32px; right: 32px;
  color: var(--accent);
  opacity: 0;
  transform: translateX(-10px);
  transition: opacity 0.3s, transform 0.3s var(--spring);
}
.service-card:hover .card-arrow {
  opacity: 1;
  transform: translateX(0);
}
.card-glow {
  position: absolute;
  bottom: -60px; left: 50%;
  transform: translateX(-50%);
  width: 120px; height: 120px;
  background: var(--accent);
  border-radius: 50%;
  filter: blur(40px);
  opacity: 0;
  transition: opacity 0.4s;
}
.service-card:hover .card-glow { opacity: 0.12; }

@media (max-width: 1000px) {
  .services { padding: 80px 40px; }
  .services-header { grid-template-columns: 1fr; gap: 20px; }
  .services-grid { grid-template-columns: repeat(2, 1fr); }
}
@media (max-width: 640px) {
  .services { padding: 60px 20px; }
  .services-grid { grid-template-columns: 1fr; }
}
</style>
