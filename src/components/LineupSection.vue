<script setup>
import { ref, computed } from 'vue'

const activeFilter = ref('all')

const artists = [
  { id: 1, name: "DAMSO", day: "day1", genre: "RAP / 92i", time: "23:00 - Main Stage", featured: true },
  { id: 2, name: "SCH", day: "day1", genre: "TRAP / CINÉMATIQUE", time: "21:30 - Main Stage", featured: false },
  { id: 3, name: "GIMS", day: "day1", genre: "RNB / RAP", time: "20:00 - West Stage", featured: false },
  { id: 4, name: "NINHO", day: "day2", genre: "RAP / DRILL", time: "23:00 - Main Stage", featured: true },
  { id: 5, name: "BOOSKA-P SHOW", day: "day2", genre: "SHOWCASE EXCLUSIF", time: "21:00 - West Stage", featured: false },
  { id: 6, name: "HAMZA", day: "day2", genre: "RNB / TRAP", time: "19:30 - Main Stage", featured: false }
]

const filteredArtists = computed(() => {
  if (activeFilter.value === 'all') return artists
  return artists.filter(artist => artist.day === activeFilter.value)
})
</script>

<template>
  <section id="lineup" class="lineup-section">
    <div class="container">
      <div class="section-header">
        <span class="badge-sub">LINE-UP OFFICIEL</span>
        <h2 class="section-title">LES TÊTES D'AFFICHE</h2>
        <p class="section-desc">Les artistes les plus lourds de la scène urbaine réunis sur 2 scènes explosives.</p>
      </div>

      <!-- BOUTONS DE FILTRE -->
      <div class="filter-buttons">
        <button 
          @click="activeFilter = 'all'" 
          :class="{ active: activeFilter === 'all' }"
          class="filter-btn"
        >
          Tous les Artistes
        </button>
        <button 
          @click="activeFilter = 'day1'" 
          :class="{ active: activeFilter === 'day1' }"
          class="filter-btn"
        >
          📅 Jour 1 (15 Juillet)
        </button>
        <button 
          @click="activeFilter = 'day2'" 
          :class="{ active: activeFilter === 'day2' }"
          class="filter-btn"
        >
          📅 Jour 2 (16 Juillet)
        </button>
      </div>

      <!-- GRILLE DES ARTISTES -->
      <div class="artists-grid">
        <div 
          v-for="artist in filteredArtists" 
          :key="artist.id" 
          class="artist-card"
          :class="{ 'featured-card': artist.featured }"
        >
          <div class="card-glow"></div>
          <div class="card-content">
            <div class="card-top">
              <span class="artist-genre">{{ artist.genre }}</span>
              <span class="artist-day">{{ artist.day === 'day1' ? 'Jour 1' : 'Jour 2' }}</span>
            </div>
            
            <h3 class="artist-name">{{ artist.name }}</h3>
            
            <div class="artist-footer">
              <span class="artist-time">🕒 {{ artist.time }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.lineup-section {
  padding: 8rem 2rem;
  background-color: #0d0d12;
  position: relative;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

.badge-sub {
  color: #ffe600;
  font-size: 0.85rem;
  font-weight: 800;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.section-title {
  font-size: 3rem;
  font-weight: 900;
  text-transform: uppercase;
  margin: 0.5rem 0 1rem 0;
  letter-spacing: -1px;
}

.section-desc {
  color: #a0a0b0;
  font-size: 1.1rem;
}

/* FILTRES */
.filter-buttons {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 3rem;
}

.filter-btn {
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #a0a0b0;
  padding: 0.7rem 1.5rem;
  border-radius: 50px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-btn:hover {
  border-color: rgba(255, 255, 255, 0.3);
  color: #fff;
}

.filter-btn.active {
  background: #ffe600;
  color: #000;
  border-color: #ffe600;
  box-shadow: 0 0 20px rgba(255, 230, 0, 0.3);
}

/* GRILLE ARTISTES */
.artists-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
}

.artist-card {
  position: relative;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 12px;
  overflow: hidden;
  height: 220px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

.artist-card:hover {
  transform: translateY(-5px);
  border-color: rgba(255, 230, 0, 0.4);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
}

.card-glow {
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, transparent 40%, rgba(255, 230, 0, 0.15) 100%);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.artist-card:hover .card-glow {
  opacity: 1;
}

.card-content {
  position: relative;
  z-index: 2;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: space-between;
}

.card-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.artist-genre {
  font-size: 0.75rem;
  font-weight: 800;
  letter-spacing: 1px;
  color: #ffe600;
  background: rgba(255, 230, 0, 0.1);
  padding: 4px 10px;
  border-radius: 4px;
}

.artist-day {
  font-size: 0.75rem;
  color: #a0a0b0;
  font-weight: 700;
}

.artist-name {
  font-size: 2.2rem;
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: -1px;
  margin: 0;
  transition: color 0.3s ease;
}

.artist-card:hover .artist-name {
  color: #ffe600;
}

.artist-footer {
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  padding-top: 1rem;
}

.artist-time {
  font-size: 0.85rem;
  color: #a0a0b0;
  font-weight: 600;
}

/* RESPONSIVE */
@media (max-width: 768px) {
  .section-title { font-size: 2.2rem; }
  .filter-buttons { flex-direction: column; align-items: stretch; }
  .artists-grid { grid-template-columns: 1fr; }
}
</style>