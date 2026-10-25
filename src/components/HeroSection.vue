<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Nom et informations de l'événement Rap / Hip-Hop
const festivalName = "OVERGROUND"
const festivalSub = "RAP & STREET CULTURE FESTIVAL"
const eventDate = "15 & 16 JUILLET 2027"
const eventLocation = "ACCOR ARENA / PARIS"

// Date cible du compte à rebours
const targetDate = new Date('2027-07-15T20:00:00').getTime()

const timeLeft = ref({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0
})

let timer = null

const updateCountdown = () => {
  const now = new Date().getTime()
  const distance = targetDate - now

  if (distance > 0) {
    timeLeft.value.days = Math.floor(distance / (1000 * 60 * 60 * 24))
    timeLeft.value.hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
    timeLeft.value.minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60))
    timeLeft.value.seconds = Math.floor((distance % (1000 * 60)) / 1000)
  }
}

onMounted(() => {
  updateCountdown()
  timer = setInterval(updateCountdown, 1000)
})

onUnmounted(() => {
  clearInterval(timer)
})
</script>

<template>
  <div class="hero-wrapper">
    <!-- BARRE DE NAVIGATION -->
    <header class="navbar">
      <div class="logo">
        <span class="logo-highlight">{{ festivalName }}</span>
        <span class="logo-badge">2027</span>
      </div>
      <nav class="nav-links">
        <a href="#lineup">Line-Up</a>
        <a href="#experience">L'Expérience</a>
        <a href="#tickets">Billetterie</a>
      </nav>
      <a href="#tickets" class="btn-primary btn-sm">Réserver</a>
    </header>

    <!-- HERO SECTION -->
    <section class="hero">
      <div class="hero-bg-effects">
        <div class="glow-sphere sphere-1"></div>
        <div class="glow-sphere sphere-2"></div>
        <div class="grid-overlay"></div>
      </div>

      <div class="hero-content">
        <div class="badge-tag">🔥 ÉDITION 2027 — 2 JOURS DE PURE URBAN VIBE</div>
        
        <h1 class="main-title">
          <span class="outline-text">THE ULTIMATE</span> <br />
          <span class="glow-text">{{ festivalName }}</span>
        </h1>
        
        <p class="subtitle">{{ festivalSub }}</p>

        <div class="meta-info">
          <div class="meta-item">📅 {{ eventDate }}</div>
          <div class="meta-divider">|</div>
          <div class="meta-item">📍 {{ eventLocation }}</div>
        </div>

        <!-- COMPTE À REBOURS -->
        <div class="countdown-container">
          <div class="countdown-item">
            <span class="number">{{ timeLeft.days }}</span>
            <span class="label">Jours</span>
          </div>
          <div class="countdown-colon">:</div>
          <div class="countdown-item">
            <span class="number">{{ String(timeLeft.hours).padStart(2, '0') }}</span>
            <span class="label">Heures</span>
          </div>
          <div class="countdown-colon">:</div>
          <div class="countdown-item">
            <span class="number">{{ String(timeLeft.minutes).padStart(2, '0') }}</span>
            <span class="label">Min</span>
          </div>
          <div class="countdown-colon">:</div>
          <div class="countdown-item">
            <span class="number">{{ String(timeLeft.seconds).padStart(2, '0') }}</span>
            <span class="label">Sec</span>
          </div>
        </div>

        <!-- BOUTONS D'ACTION -->
        <div class="cta-group">
          <a href="#tickets" class="btn-primary btn-lg">Prendre mon Pass →</a>
          <a href="#lineup" class="btn-secondary btn-lg">Voir le Line-Up</a>
        </div>
      </div>
    </section>

    <!-- BANNIÈRE DÉFILANTE -->
    <div class="marquee-wrapper">
      <div class="marquee-content">
        <span>⚡ 100% TRAP & DRILL ⚡ HEADLINERS EXCLUSIFS ⚡ VIP EXPERIENCE ⚡ BEATS & GRAFFITI ⚡</span>
        <span>⚡ 100% TRAP & DRILL ⚡ HEADLINERS EXCLUSIFS ⚡ VIP EXPERIENCE ⚡ BEATS & GRAFFITI ⚡</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.hero-wrapper {
  position: relative;
  width: 100%;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.2rem 4rem;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 100;
  background: rgba(10, 10, 14, 0.8);
  backdrop-filter: blur(15px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.logo {
  font-weight: 900;
  font-size: 1.6rem;
  letter-spacing: -1px;
}

.logo-highlight { color: #ffe600; }
.logo-badge {
  background: #ff2a54;
  color: #000;
  font-size: 0.7rem;
  padding: 2px 6px;
  border-radius: 4px;
  margin-left: 6px;
  vertical-align: super;
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-links a {
  color: #a0a0b0;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s;
}

.nav-links a:hover { color: #ffe600; }

.btn-primary {
  background: #ffe600;
  color: #000;
  font-weight: 800;
  padding: 0.8rem 1.8rem;
  border-radius: 4px;
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 1px;
  display: inline-flex;
  align-items: center;
  transition: all 0.3s ease;
  box-shadow: 0 0 20px rgba(255, 230, 0, 0.3);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 0 30px rgba(255, 230, 0, 0.6);
}

.btn-secondary {
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: #fff;
  font-weight: 700;
  padding: 0.8rem 1.8rem;
  border-radius: 4px;
  text-decoration: none;
  text-transform: uppercase;
  transition: all 0.3s ease;
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: #fff;
}

.btn-sm { padding: 0.5rem 1.2rem; font-size: 0.85rem; }
.btn-lg { padding: 1rem 2.2rem; font-size: 1rem; }

.hero {
  position: relative;
  min-height: 90vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 9rem 2rem 5rem 2rem;
  text-align: center;
}

.hero-bg-effects {
  position: absolute;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
}

.glow-sphere {
  position: absolute;
  border-radius: 50%;
  filter: blur(120px);
  opacity: 0.3;
}

.sphere-1 { width: 450px; height: 450px; background: #ffe600; top: 10%; left: 10%; }
.sphere-2 { width: 500px; height: 500px; background: #ff2a54; bottom: 10%; right: 10%; }

.grid-overlay {
  position: absolute;
  inset: 0;
  background-image: linear-gradient(rgba(255, 255, 255, 0.03) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
}

.hero-content {
  position: relative;
  z-index: 10;
  max-width: 900px;
}

.badge-tag {
  display: inline-block;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.15);
  padding: 0.5rem 1.2rem;
  border-radius: 50px;
  font-size: 0.85rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
}

.main-title {
  font-size: 5rem;
  font-weight: 900;
  line-height: 0.95;
  letter-spacing: -2px;
  margin-bottom: 1rem;
}

.outline-text {
  color: transparent;
  -webkit-text-stroke: 2px rgba(255, 255, 255, 0.8);
}

.glow-text {
  color: #ffe600;
  text-shadow: 0 0 35px rgba(255, 230, 0, 0.5);
}

.subtitle {
  font-size: 1.2rem;
  letter-spacing: 3px;
  color: #a0a0b0;
  margin-bottom: 2rem;
  font-weight: 800;
}

.meta-info {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.5rem;
  font-size: 1.1rem;
  font-weight: 700;
  margin-bottom: 2.5rem;
}

.meta-divider { color: rgba(255, 255, 255, 0.2); }

.countdown-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.5rem;
  margin: 0 auto 3rem auto;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 1.2rem 2.5rem;
  border-radius: 12px;
  backdrop-filter: blur(10px);
  width: fit-content;
}

.countdown-item { display: flex; flex-direction: column; align-items: center; }
.countdown-item .number { font-size: 2.5rem; font-weight: 900; font-variant-numeric: tabular-nums; }
.countdown-item .label { font-size: 0.75rem; color: #a0a0b0; text-transform: uppercase; }
.countdown-colon { font-size: 2rem; font-weight: 900; color: #ffe600; margin-top: -15px; }

.cta-group { display: flex; justify-content: center; gap: 1.5rem; }

.marquee-wrapper {
  background: #ffe600;
  color: #000;
  padding: 0.8rem 0;
  overflow: hidden;
  white-space: nowrap;
  font-weight: 900;
  letter-spacing: 2px;
  transform: rotate(-1deg);
}

.marquee-content {
  display: inline-block;
  animation: marquee 20s linear infinite;
}

.marquee-content span { padding-right: 2rem; }

@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

@media (max-width: 768px) {
  .navbar { padding: 1rem 1.5rem; }
  .nav-links { display: none; }
  .main-title { font-size: 3rem; }
  .meta-info { flex-direction: column; gap: 0.5rem; }
  .meta-divider { display: none; }
  .countdown-container { gap: 0.8rem; padding: 1rem; }
  .countdown-item .number { font-size: 1.8rem; }
  .cta-group { flex-direction: column; }
}
</style>