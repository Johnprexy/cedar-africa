<template>
  <section class="hero noise" id="hero">
    <!-- Animated background -->
    <div class="hero-bg">
      <div class="orb orb-1"></div>
      <div class="orb orb-2"></div>
      <div class="orb orb-3"></div>
      <div class="grid-lines"></div>
    </div>

    <!-- Floating badge -->
    <div class="hero-badge reveal reveal-delay-1" ref="badge">
      <span class="section-label">Est. 2024 · Lagos & London</span>
    </div>

    <!-- Main copy -->
    <div class="hero-content">
      <h1 class="hero-title">
        <span class="line reveal" ref="line1">Your Dream Home</span>
        <span class="line accent reveal reveal-delay-1" ref="line2">
          <em>in Nigeria.</em>
          <svg class="title-deco" viewBox="0 0 200 40" fill="none">
            <path d="M0 35 Q50 5 100 30 Q150 55 200 20" stroke="var(--gold)" stroke-width="2" fill="none" stroke-dasharray="240" stroke-dashoffset="240">
              <animate attributeName="stroke-dashoffset" from="240" to="0" dur="1.2s" begin="0.8s" fill="freeze" calcMode="spline" keySplines="0.16 1 0.3 1"/>
            </path>
          </svg>
        </span>
        <span class="line reveal reveal-delay-2" ref="line3">Built From Anywhere.</span>
      </h1>

      <p class="hero-sub reveal reveal-delay-3">
        We're the trusted bridge between the diaspora and their land back home — handling everything from acquisition to construction, so you never miss a brick.
      </p>

      <div class="hero-actions reveal reveal-delay-4">
        <a href="#booking" class="btn-primary" @mouseenter="$emit('hover')" @mouseleave="$emit('unhover')">
          <span>Book a Free Consultation</span>
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
            <path d="M4 10H16M10 4L16 10L10 16" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
        </a>
        <a href="#process" class="btn-ghost" @mouseenter="$emit('hover')" @mouseleave="$emit('unhover')">
          <span>See how it works</span>
        </a>
      </div>

      <!-- Stats row -->
      <div class="hero-stats reveal reveal-delay-5">
        <div class="stat" v-for="s in stats" :key="s.label">
          <span class="stat-num">{{ s.num }}</span>
          <span class="stat-label">{{ s.label }}</span>
        </div>
      </div>
    </div>

    <!-- Right image collage -->
    <div class="hero-visual reveal reveal-delay-2">
      <div class="visual-frame">
        <div class="img-main">
          <img src="https://images.unsplash.com/photo-1600596542815-ffad4c1539a9?w=600&q=80" alt="Beautiful Nigerian home" />
          <div class="img-overlay"></div>
        </div>
        <div class="img-float img-float-1">
          <img src="https://images.unsplash.com/photo-1512917774080-9991f1c4c750?w=300&q=80" alt="Modern architecture" />
        </div>
        <div class="img-float img-float-2">
          <img src="https://images.unsplash.com/photo-1523217582562-09d0def993a6?w=300&q=80" alt="Interior design" />
        </div>
        <div class="trust-badge">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
            <path d="M10 2L12.4 7.6L18.5 8.3L14.1 12.5L15.3 18.5L10 15.6L4.7 18.5L5.9 12.5L1.5 8.3L7.6 7.6L10 2Z" fill="var(--gold)"/>
          </svg>
          <div>
            <strong>Trusted by 200+</strong>
            <span>diaspora families</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll cue -->
    <div class="scroll-cue">
      <div class="scroll-line"></div>
      <span>Scroll</span>
    </div>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue'
defineEmits(['hover', 'unhover'])

const stats = [
  { num: '200+', label: 'Projects completed' },
  { num: '12+', label: 'Years experience' },
  { num: '6', label: 'Countries served' },
]

onMounted(() => {
  const els = document.querySelectorAll('.reveal')
  setTimeout(() => { els.forEach(el => el.classList.add('visible')) }, 100)
})
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  gap: 60px;
  padding: 140px 80px 80px;
  background: var(--forest-deep);
  position: relative;
  overflow: hidden;
}

.hero-bg { position: absolute; inset: 0; pointer-events: none; }
.orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  animation: float 8s ease-in-out infinite;
}
.orb-1 { width: 500px; height: 500px; background: rgba(201,168,76,0.08); top: -150px; right: -100px; animation-delay: 0s; }
.orb-2 { width: 400px; height: 400px; background: rgba(44,80,64,0.3); bottom: -100px; left: -100px; animation-delay: 3s; }
.orb-3 { width: 300px; height: 300px; background: rgba(201,168,76,0.05); top: 40%; left: 30%; animation-delay: 5s; }
.grid-lines {
  position: absolute;
  inset: 0;
  background-image: linear-gradient(rgba(201,168,76,0.04) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(201,168,76,0.04) 1px, transparent 1px);
  background-size: 60px 60px;
}
@keyframes float {
  0%, 100% { transform: translateY(0) scale(1); }
  50% { transform: translateY(-30px) scale(1.05); }
}

.hero-badge {
  position: absolute;
  top: 120px; left: 80px;
  display: flex;
  align-items: center;
  gap: 10px;
}
.hero-badge::before {
  content: '';
  display: block;
  width: 40px;
  height: 1px;
  background: var(--gold);
}

.hero-content {
  position: relative;
  z-index: 2;
}

.hero-title {
  font-family: var(--font-display);
  font-size: clamp(3rem, 5vw, 5rem);
  font-weight: 300;
  line-height: 1.08;
  color: var(--cream);
  margin-bottom: 28px;
  margin-top: 40px;
}
.hero-title .line { display: block; }
.hero-title .accent { color: var(--gold-light); font-style: italic; position: relative; }
.title-deco {
  position: absolute;
  bottom: -12px; left: 0;
  width: 100%;
  height: 40px;
}

.hero-sub {
  font-size: 1.05rem;
  line-height: 1.75;
  color: rgba(247,242,232,0.65);
  max-width: 480px;
  margin-bottom: 44px;
  font-weight: 300;
}

.hero-actions {
  display: flex;
  gap: 20px;
  align-items: center;
  flex-wrap: wrap;
  margin-bottom: 56px;
}

.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  font-family: var(--font-ui);
  font-size: 0.82rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  text-decoration: none;
  color: var(--forest-deep);
  background: var(--gold);
  padding: 16px 32px;
  transition: background 0.3s, transform 0.3s var(--spring), box-shadow 0.3s;
}
.btn-primary:hover {
  background: var(--gold-light);
  transform: translateY(-2px);
  box-shadow: 0 20px 40px rgba(201,168,76,0.3);
}
.btn-ghost {
  font-family: var(--font-ui);
  font-size: 0.82rem;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-decoration: none;
  color: var(--cream);
  opacity: 0.6;
  border-bottom: 1px solid rgba(247,242,232,0.3);
  padding-bottom: 2px;
  transition: opacity 0.3s, border-color 0.3s;
}
.btn-ghost:hover { opacity: 1; border-color: var(--gold); color: var(--gold); }

.hero-stats {
  display: flex;
  gap: 48px;
  padding-top: 40px;
  border-top: 1px solid rgba(247,242,232,0.1);
}
.stat { display: flex; flex-direction: column; gap: 4px; }
.stat-num {
  font-family: var(--font-display);
  font-size: 2rem;
  font-weight: 600;
  color: var(--gold);
  line-height: 1;
}
.stat-label {
  font-size: 0.78rem;
  color: rgba(247,242,232,0.45);
  font-weight: 300;
  letter-spacing: 0.02em;
}

/* Visual collage */
.hero-visual {
  position: relative;
  z-index: 2;
  height: 580px;
}
.visual-frame { position: relative; width: 100%; height: 100%; }
.img-main {
  position: absolute;
  top: 0; right: 0;
  width: 80%;
  height: 70%;
  overflow: hidden;
}
.img-main img { width: 100%; height: 100%; object-fit: cover; transition: transform 8s ease; }
.img-main:hover img { transform: scale(1.05); }
.img-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(15,33,25,0.3) 0%, transparent 60%);
}
.img-float {
  position: absolute;
  overflow: hidden;
  box-shadow: 0 30px 60px rgba(0,0,0,0.4);
}
.img-float img { width: 100%; height: 100%; object-fit: cover; }
.img-float-1 {
  width: 180px; height: 160px;
  bottom: 80px; left: 0;
  animation: floatCard 6s ease-in-out infinite;
}
.img-float-2 {
  width: 150px; height: 130px;
  bottom: 0; right: 10%;
  animation: floatCard 6s ease-in-out infinite 2s;
}
@keyframes floatCard {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-12px); }
}

.trust-badge {
  position: absolute;
  top: 20%; left: 0;
  background: var(--gold);
  padding: 14px 18px;
  display: flex;
  align-items: center;
  gap: 12px;
  box-shadow: 0 20px 40px rgba(0,0,0,0.3);
  animation: floatCard 5s ease-in-out infinite 1s;
}
.trust-badge div { display: flex; flex-direction: column; gap: 2px; }
.trust-badge strong { font-family: var(--font-ui); font-size: 0.85rem; color: var(--forest-deep); }
.trust-badge span { font-size: 0.72rem; color: var(--forest); opacity: 0.7; }

.scroll-cue {
  position: absolute;
  bottom: 40px; left: 80px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}
.scroll-line {
  width: 1px;
  height: 60px;
  background: linear-gradient(to bottom, var(--gold), transparent);
  animation: scrollPulse 2s ease-in-out infinite;
}
@keyframes scrollPulse {
  0%, 100% { opacity: 0.3; transform: scaleY(1); }
  50% { opacity: 1; transform: scaleY(1.1); }
}
.scroll-cue span {
  font-family: var(--font-ui);
  font-size: 0.62rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: rgba(247,242,232,0.35);
  writing-mode: vertical-rl;
}

@media (max-width: 1000px) {
  .hero {
    grid-template-columns: 1fr;
    padding: 120px 40px 80px;
    gap: 40px;
  }
  .hero-badge { left: 40px; }
  .hero-visual { height: 360px; }
  .scroll-cue { left: 40px; bottom: 20px; }
}
@media (max-width: 600px) {
  .hero { padding: 100px 20px 60px; }
  .hero-badge { left: 20px; top: 100px; }
  .hero-title { font-size: 2.8rem; }
  .hero-stats { gap: 28px; }
  .scroll-cue { display: none; }
}
</style>
