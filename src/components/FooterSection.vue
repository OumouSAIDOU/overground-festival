<script setup>
import { ref } from 'vue'

const email = ref('')

const subscribeNewsletter = () => {
  if (!email.value) {
    alert("Veuillez entrer une adresse e-mail valide.")
    return
  }
  alert(`Merci ! ${email.value} a bien été inscrit à la newsletter du festival.`)
  email.value = ''
}
</script>

<template>
  <footer class="footer">
    <div class="container">
      <!-- NEWSLETTER SECTION -->
      <div class="newsletter-box">
        <div class="newsletter-content">
          <h3>RESTÉS INFORMÉS DE LA PROGRAMMATION</h3>
          <p>Inscris-toi pour recevoir les annonces d'artistes secrets et les offres exclusives.</p>
        </div>
        <form @submit.prevent="subscribeNewsletter" class="newsletter-form">
          <input 
            v-model="email" 
            type="email" 
            placeholder="Ton adresse e-mail..." 
            required
          />
          <button type="submit" class="btn-subscribe">S'inscrire</button>
        </form>
      </div>

      <div class="footer-main">
        <!-- LOGO & INFOS -->
        <div class="footer-brand">
          <div class="logo">
            <span class="logo-highlight">OVERGROUND</span>
            <span class="logo-badge">2027</span>
          </div>
          <p class="brand-desc">
            Le plus grand rassemblement Rap & Street Culture à Paris. 2 jours d'immersion totale dans l'univers urbain.
          </p>
        </div>

        <!-- NAVIGATION RAPIDE -->
        <div class="footer-links">
          <h4>Navigation</h4>
          <ul>
            <li><a href="#lineup">Line-Up</a></li>
            <li><a href="#tickets">Billetterie</a></li>
            <li><a href="#experience">Infos Pratiques</a></li>
          </ul>
        </div>

        <!-- RÉSEAUX SOCIAUX -->
        <div class="footer-socials">
          <h4>Suis-nous</h4>
          <div class="social-icons">
            <a href="#" class="social-btn">INSTAGRAM</a>
            <a href="#" class="social-btn">TIKTOK</a>
            <a href="#" class="social-btn">YOUTUBE</a>
            <a href="#" class="social-btn">SPOTIFY</a>
          </div>
        </div>
      </div>

      <!-- COPYRIGHT & MENTIONS -->
      <div class="footer-bottom">
        <p>© 2027 OVERGROUND FESTIVAL. Tous droits réservés.</p>
        <div class="legal-links">
          <a href="#">Mentions Légales</a>
          <a href="#">CGV</a>
          <a href="#">Politique de Confidentialité</a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background-color: #060608;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  padding: 5rem 2rem 2rem 2rem;
  color: #a0a0b0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

/* NEWSLETTER */
.newsletter-box {
  background: linear-gradient(135deg, rgba(255, 230, 0, 0.08) 0%, rgba(255, 42, 84, 0.08) 100%);
  border: 1px solid rgba(255, 230, 0, 0.2);
  border-radius: 16px;
  padding: 3rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 2rem;
  margin-bottom: 5rem;
}

.newsletter-content h3 {
  color: #fff;
  font-size: 1.5rem;
  font-weight: 900;
  margin-bottom: 0.5rem;
}

.newsletter-content p {
  font-size: 0.95rem;
}

.newsletter-form {
  display: flex;
  gap: 0.8rem;
  min-width: 350px;
}

.newsletter-form input {
  flex: 1;
  background: rgba(0, 0, 0, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.15);
  padding: 0.8rem 1.2rem;
  border-radius: 6px;
  color: #fff;
  font-size: 0.95rem;
  outline: none;
}

.newsletter-form input:focus {
  border-color: #ffe600;
}

.btn-subscribe {
  background: #ffe600;
  color: #000;
  font-weight: 800;
  padding: 0.8rem 1.5rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  text-transform: uppercase;
  transition: opacity 0.2s;
}

.btn-subscribe:hover {
  opacity: 0.9;
}

/* FOOTER MAIN */
.footer-main {
  display: grid;
  grid-template-columns: 2fr 1fr 1.5fr;
  gap: 4rem;
  margin-bottom: 4rem;
}

.logo {
  font-weight: 900;
  font-size: 1.5rem;
  margin-bottom: 1rem;
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

.brand-desc {
  line-height: 1.6;
  font-size: 0.95rem;
  max-width: 350px;
}

.footer-main h4 {
  color: #fff;
  font-weight: 800;
  font-size: 1.1rem;
  margin-bottom: 1.2rem;
  text-transform: uppercase;
}

.footer-links ul {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.footer-links a {
  color: #a0a0b0;
  text-decoration: none;
  transition: color 0.2s;
}

.footer-links a:hover {
  color: #ffe600;
}

.social-icons {
  display: flex;
  flex-wrap: wrap;
  gap: 0.8rem;
}

.social-btn {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #fff;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 800;
  text-decoration: none;
  transition: all 0.3s;
}

.social-btn:hover {
  background: #ffe600;
  color: #000;
  border-color: #ffe600;
}

/* FOOTER BOTTOM */
.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  padding-top: 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.85rem;
}

.legal-links {
  display: flex;
  gap: 1.5rem;
}

.legal-links a {
  color: #a0a0b0;
  text-decoration: none;
}

.legal-links a:hover {
  color: #fff;
}

@media (max-width: 900px) {
  .newsletter-box { flex-direction: column; text-align: center; }
  .newsletter-form { min-width: 100%; flex-direction: column; }
  .footer-main { grid-template-columns: 1fr; gap: 2.5rem; }
  .footer-bottom { flex-direction: column; gap: 1rem; text-align: center; }
}
</style>