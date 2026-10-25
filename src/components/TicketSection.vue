<script setup>
import { ref, computed } from 'vue'

// Liste des offres de tickets disponibles
const tickets = ref([
  {
    id: 'day1',
    name: 'PASS 1 JOUR',
    date: 'Samedi 15 Juillet',
    price: 65,
    description: 'Accès complet à toutes les scènes et animations pour le Jour 1.',
    quantity: 0
  },
  {
    id: 'day2',
    name: 'PASS 2 JOURS',
    date: '15 & 16 Juillet',
    price: 110,
    description: 'Le pass ultime pour ne rien rater du week-end complet.',
    quantity: 0
  },
  {
    id: 'vip',
    name: 'PASS VIP GOLD',
    date: 'Pass 2 Jours + Avantages',
    price: 190,
    description: 'Accès fosse VIP, espace lounge privé, coupe-file et open bar softs.',
    quantity: 0
  }
])

// Fonctions pour incrémenter / décrémenter la quantité
const increment = (ticket) => {
  ticket.quantity++
}

const decrement = (ticket) => {
  if (ticket.quantity > 0) {
    ticket.quantity--
  }
}

// Calcul du montant total en temps réel
const totalPrice = computed(() => {
  return tickets.value.reduce((sum, t) => sum + (t.price * t.quantity), 0)
})

// Calcul du nombre total de tickets sélectionnés
const totalTicketsCount = computed(() => {
  return tickets.value.reduce((sum, t) => sum + t.quantity, 0)
})

// Simulation du checkout
const checkout = () => {
  if (totalTicketsCount.value === 0) {
    alert("Veuillez sélectionner au moins un pass !")
    return
  }
  alert(`Commande validée ! Total : ${totalPrice.value}€. Redirection vers le paiement sécurisé...`)
}
</script>

<template>
  <section id="tickets" class="ticket-section">
    <div class="container">
      <div class="section-header">
        <span class="badge-sub">BILLETTERIE OFFICIELLE</span>
        <h2 class="section-title">CHOISISSEZ VOTRE PASS</h2>
        <p class="section-desc">Les places sont limitées. Réservez dès maintenant pour garantir votre accès.</p>
      </div>

      <!-- CARTES DE TICKETS -->
      <div class="tickets-grid">
        <div v-for="ticket in tickets" :key="ticket.id" class="ticket-card" :class="{ 'vip-card': ticket.id === 'vip' }">
          <div v-if="ticket.id === 'vip'" class="vip-badge">ULTIMATE VIP</div>
          
          <div class="ticket-info">
            <span class="ticket-date">{{ ticket.date }}</span>
            <h3 class="ticket-name">{{ ticket.name }}</h3>
            <p class="ticket-desc">{{ ticket.description }}</p>
            <div class="ticket-price">{{ ticket.price }}€</div>
          </div>

          <!-- CONTRÔLE DE QUANTITÉ -->
          <div class="ticket-action">
            <div class="quantity-selector">
              <button @click="decrement(ticket)" :disabled="ticket.quantity === 0" class="qty-btn">-</button>
              <span class="qty-value">{{ ticket.quantity }}</span>
              <button @click="increment(ticket)" class="qty-btn">+</button>
            </div>
          </div>
        </div>
      </div>

      <!-- PANIER FLOTTANT / RÉCAPITULATIF -->
      <div class="checkout-bar" v-if="totalTicketsCount > 0">
        <div class="checkout-info">
          <span class="summary-count">{{ totalTicketsCount }} pass sélectionné(s)</span>
          <span class="summary-total">Total : <strong>{{ totalPrice }}€</strong></span>
        </div>
        <button @click="checkout" class="btn-primary btn-checkout">
          <span>Valider ma commande</span>
          <span>→</span>
        </button>
      </div>
    </div>
  </section>
</template>

<style scoped>
.ticket-section {
  padding: 8rem 2rem;
  background-color: #0a0a0e;
  position: relative;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  min-height: 90vh;
}

.container {
  max-width: 1200px;
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

/* GRILLE TICKETS */
.tickets-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 2rem;
  margin-bottom: 6rem;
}

.ticket-card {
  position: relative;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  padding: 2.5rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: all 0.3s ease;
}

.ticket-card:hover {
  border-color: rgba(255, 255, 255, 0.2);
  transform: translateY(-5px);
}

.vip-card {
  background: linear-gradient(135deg, rgba(255, 230, 0, 0.05) 0%, rgba(255, 42, 84, 0.05) 100%);
  border-color: rgba(255, 230, 0, 0.3);
}

.vip-badge {
  position: absolute;
  top: -12px;
  right: 2rem;
  background: #ffe600;
  color: #000;
  font-size: 0.7rem;
  font-weight: 900;
  padding: 4px 10px;
  border-radius: 20px;
  letter-spacing: 1px;
}

.ticket-date {
  font-size: 0.8rem;
  font-weight: 700;
  color: #a0a0b0;
  text-transform: uppercase;
}

.ticket-name {
  font-size: 2rem;
  font-weight: 900;
  margin: 0.5rem 0 1rem 0;
  letter-spacing: -1px;
}

.ticket-desc {
  color: #a0a0b0;
  font-size: 0.95rem;
  line-height: 1.5;
  margin-bottom: 2rem;
}

.ticket-price {
  font-size: 2.5rem;
  font-weight: 900;
  color: #ffe600;
  margin-bottom: 2rem;
}

/* QUANTITY SELECTOR */
.ticket-action {
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  padding-top: 1.5rem;
  display: flex;
  justify-content: center;
}

.quantity-selector {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 0.4rem 1rem;
  border-radius: 50px;
}

.qty-btn {
  background: none;
  border: none;
  color: #fff;
  font-size: 1.2rem;
  font-weight: 900;
  cursor: pointer;
  transition: color 0.2s;
}

.qty-btn:hover:not(:disabled) {
  color: #ffe600;
}

.qty-btn:disabled {
  color: #444;
  cursor: not-allowed;
}

.qty-value {
  font-size: 1.2rem;
  font-weight: 900;
  min-width: 25px;
  text-align: center;
}

/* PANIER FLOTTANT (CHECKOUT BAR) */
.checkout-bar {
  position: fixed;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  width: 90%;
  max-width: 700px;
  background: rgba(15, 15, 20, 0.9);
  border: 1px solid rgba(255, 230, 0, 0.4);
  backdrop-filter: blur(20px);
  padding: 1.2rem 2.5rem;
  border-radius: 50px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.8), 0 0 20px rgba(255, 230, 0, 0.2);
  z-index: 1000;
  animation: slideUp 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.checkout-info {
  display: flex;
  flex-direction: column;
}

.summary-count {
  font-size: 0.8rem;
  color: #a0a0b0;
  font-weight: 600;
}

.summary-total {
  font-size: 1.3rem;
  color: #fff;
}

.summary-total strong {
  color: #ffe600;
}

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
  gap: 10px;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 0 20px rgba(255, 230, 0, 0.3);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 0 30px rgba(255, 230, 0, 0.6);
}

@keyframes slideUp {
  from { transform: translate(-50%, 50px); opacity: 0; }
  to { transform: translate(-50%, 0); opacity: 1; }
}

@media (max-width: 768px) {
  .section-title { font-size: 2.2rem; }
  .checkout-bar { flex-direction: column; gap: 1rem; border-radius: 16px; text-align: center; padding: 1.5rem; }
  .checkout-info { align-items: center; }
}
</style>