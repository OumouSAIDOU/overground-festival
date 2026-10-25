<script setup>
import { ref } from 'vue'

// Liste des questions / réponses
const faqs = ref([
  {
    id: 1,
    question: "Comment accéder au festival Overground ?",
    answer: "L'événement se déroule à l'Accor Arena de Paris (Bercy). Vous pouvez y accéder facilement via la ligne 6 ou 14 du métro (station Bercy) ou par le RER A (Gare de Lyon, à 10 min à pied).",
    isOpen: false
  },
  {
    id: 2,
    question: "Y a-t-il un âge minimum requis ?",
    answer: "L'événement est accessible à partir de 16 ans. Les mineurs de moins de 16 ans doivent être obligatoirement accompagnés d'un tuteur légal muni d'un billet valide.",
    isOpen: false
  },
  {
    id: 3,
    question: "Dois-je imprimer mon e-ticket ?",
    answer: "Non, inutile d'imprimer ! Présentez simplement le QR code de votre e-ticket directement depuis votre smartphone à l'entrée avec une pièce d'identité.",
    isOpen: false
  },
  {
    id: 4,
    question: "Quels sont les avantages du Pass VIP Gold ?",
    answer: "Le Pass VIP vous donne un accès coupe-file à l'entrée, l'accès à la Fosse VIP juste devant la scène, un bar/lounge réservé et un pack de goodies exclusif.",
    isOpen: false
  },
  {
    id: 5,
    question: "Puis-je sortir et re-rentrer pendant le festival ?",
    answer: "Toute sortie du site est définitive pour la journée. Assurez-vous d'avoir tout ce dont vous avez besoin avec vous avant de passer le contrôle.",
    isOpen: false
  }
])

// Fonction pour ouvrir / fermer un accordéon
const toggleFaq = (index) => {
  faqs.value[index].isOpen = !faqs.value[index].isOpen
}
</script>

<template>
  <section id="experience" class="faq-section">
    <div class="container">
      <div class="section-header">
        <span class="badge-sub">INFOS PRATIQUES</span>
        <h2 class="section-title">QUESTIONS FRÉQUENTES</h2>
        <p class="section-desc">Tout ce qu'il faut savoir avant de venir retourner le festival.</p>
      </div>

      <!-- INFOS CLÉS EN CARTES -->
      <div class="info-grid">
        <div class="info-card">
          <div class="info-icon">📍</div>
          <h3>Lieu & Accès</h3>
          <p>Accor Arena, Paris Bercy<br />Lignes 6 & 14 — Station Bercy</p>
        </div>
        <div class="info-card">
          <div class="info-icon">🕒</div>
          <h3>Horaires</h3>
          <p>Ouverture des portes : 16h00<br />Début des concerts : 17h30</p>
        </div>
        <div class="info-card">
          <div class="info-icon">🍔</div>
          <h3>Food & Drinks</h3>
          <p>Foodtrucks street-food, options végé & bars sur place.</p>
        </div>
      </div>

      <!-- ACCORDÉON FAQ -->
      <div class="faq-accordion">
        <div 
          v-for="(faq, index) in faqs" 
          :key="faq.id" 
          class="faq-item"
          :class="{ open: faq.isOpen }"
          @click="toggleFaq(index)"
        >
          <div class="faq-question">
            <h3>{{ faq.question }}</h3>
            <span class="faq-icon">{{ faq.isOpen ? '−' : '+' }}</span>
          </div>
          <div v-if="faq.isOpen" class="faq-answer">
            <p>{{ faq.answer }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.faq-section {
  padding: 8rem 2rem;
  background-color: #0d0d12;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.container {
  max-width: 1000px;
  margin: 0 auto;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
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

/* GRILLE INFOS PRATIQUES */
.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.5rem;
  margin-bottom: 4rem;
}

.info-card {
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.08);
  padding: 2rem;
  border-radius: 12px;
  text-align: center;
  transition: border-color 0.3s;
}

.info-card:hover {
  border-color: rgba(255, 230, 0, 0.3);
}

.info-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.info-card h3 {
  font-size: 1.2rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
}

.info-card p {
  color: #a0a0b0;
  font-size: 0.95rem;
  line-height: 1.5;
}

/* ACCORDÉON FAQ */
.faq-accordion {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.faq-item {
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 10px;
  padding: 1.5rem 2rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.faq-item:hover {
  border-color: rgba(255, 255, 255, 0.2);
}

.faq-item.open {
  border-color: #ffe600;
  background: rgba(255, 230, 0, 0.02);
}

.faq-question {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.faq-question h3 {
  font-size: 1.1rem;
  font-weight: 700;
  margin: 0;
}

.faq-icon {
  font-size: 1.5rem;
  font-weight: 900;
  color: #ffe600;
}

.faq-answer {
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  color: #a0a0b0;
  line-height: 1.6;
  font-size: 0.95rem;
}

@media (max-width: 768px) {
  .section-title { font-size: 2.2rem; }
  .faq-item { padding: 1.2rem; }
}
</style>