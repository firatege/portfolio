<script setup>
import { Github, Linkedin, Twitter, Heart, ArrowUp } from 'lucide-vue-next'

const socialLinks = [
  { name: 'GitHub', icon: Github, url: 'https://github.com/firatege' },
  { name: 'LinkedIn', icon: Linkedin, url: 'https://www.linkedin.com/in/byfeb' },
  { name: 'X', icon: Twitter, url: 'https://x.com/FratEgeBayram1' }
]

const navLinks = [
  { name: 'About', href: '#about' },
  { name: 'Skills', href: '#skills' },
  { name: 'Experience', href: '#experience' },
  { name: 'Projects', href: '#projects' },
  { name: 'Contact', href: '#contact' }
]

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <footer class="footer">
    <div class="footer-content">
      <!-- Logo & Description -->
      <div class="footer-brand">
        <div class="brand-logo">FEB</div>
        <p class="brand-desc">
          Computer Science Student & Developer focused on building data-driven systems and scalable software.
        </p>
      </div>

      <!-- Quick Links -->
      <div class="footer-links">
        <h4>Quick Links</h4>
        <nav>
          <a v-for="link in navLinks" :key="link.name" :href="link.href">
            {{ link.name }}
          </a>
        </nav>
      </div>

      <!-- Social Links -->
      <div class="footer-social">
        <h4>Connect</h4>
        <div class="social-icons">
          <a
            v-for="social in socialLinks"
            :key="social.name"
            :href="social.url"
            target="_blank"
            :title="social.name"
          >
            <component :is="social.icon" :size="20" />
          </a>
        </div>
      </div>
    </div>

    <!-- Bottom Bar -->
    <div class="footer-bottom">
      <p>
        <span>© 2026 Fırat Ege Bayram. Made with</span>
        <Heart :size="14" class="heart-icon" />
        <span>and Vue.js</span>
      </p>

      <!-- Back to Top -->
      <button class="back-to-top" @click="scrollToTop" title="Back to top">
        <ArrowUp :size="18" />
      </button>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  position: relative;
  padding: 4rem 2rem 0;
  background: linear-gradient(180deg, #070d15 0%, #050a10 100%);
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 3rem;
  padding-bottom: 3rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

/* Brand */
.footer-brand {
  max-width: 300px;
}

.brand-logo {
  font-family: 'Fira Code', monospace;
  font-size: 2rem;
  font-weight: 700;
  background: linear-gradient(135deg, #22d3ee, #10b981);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  margin-bottom: 1rem;
}

.brand-desc {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.5);
  line-height: 1.6;
}

/* Links */
.footer-links h4,
.footer-social h4 {
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 1.25rem;
  font-weight: 600;
}

.footer-links nav {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.footer-links a {
  color: rgba(255, 255, 255, 0.5);
  text-decoration: none;
  font-size: 0.9rem;
  transition: all 0.2s ease;
}

.footer-links a:hover {
  color: #22d3ee;
  transform: translateX(5px);
}

/* Social */
.social-icons {
  display: flex;
  gap: 0.75rem;
}

.social-icons a {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 10px;
  color: rgba(255, 255, 255, 0.6);
  transition: all 0.3s ease;
}

.social-icons a:hover {
  background: rgba(34, 211, 238, 0.1);
  border-color: rgba(34, 211, 238, 0.3);
  color: #22d3ee;
  transform: translateY(-3px);
}

/* Bottom Bar */
.footer-bottom {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1.5rem 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-bottom p {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.4);
}

.heart-icon {
  color: #ef4444;
  animation: heartbeat 1.5s ease-in-out infinite;
}

@keyframes heartbeat {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.2); }
}

/* Back to Top */
.back-to-top {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  color: rgba(255, 255, 255, 0.6);
  cursor: pointer;
  transition: all 0.3s ease;
}

.back-to-top:hover {
  background: rgba(34, 211, 238, 0.1);
  border-color: rgba(34, 211, 238, 0.3);
  color: #22d3ee;
  transform: translateY(-3px);
}

/* Responsive */
@media (max-width: 768px) {
  .footer {
    padding: 3rem 1.5rem 0;
  }

  .footer-content {
    grid-template-columns: 1fr;
    gap: 2rem;
    text-align: center;
  }

  .footer-brand {
    max-width: 100%;
  }

  .brand-logo {
    font-size: 1.75rem;
  }

  .brand-desc {
    font-size: 0.85rem;
  }

  .footer-links h4,
  .footer-social h4 {
    font-size: 0.95rem;
    margin-bottom: 1rem;
  }

  .footer-links nav {
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
  }

  .footer-links a:hover {
    transform: none;
  }

  .social-icons {
    justify-content: center;
  }

  .footer-bottom {
    flex-direction: column;
    gap: 1rem;
    padding: 1.25rem 0;
  }
}

@media (max-width: 640px) {
  .footer {
    padding: 2.5rem 1rem 0;
  }

  .footer-content {
    gap: 1.5rem;
    padding-bottom: 2rem;
  }

  .brand-logo {
    font-size: 1.5rem;
    margin-bottom: 0.75rem;
  }

  .brand-desc {
    font-size: 0.8rem;
    line-height: 1.5;
  }

  .footer-links h4,
  .footer-social h4 {
    font-size: 0.9rem;
    margin-bottom: 0.75rem;
  }

  .footer-links nav {
    gap: 0.75rem;
  }

  .footer-links a {
    font-size: 0.85rem;
    padding: 0.25rem 0.5rem;
  }

  .social-icons {
    gap: 0.5rem;
  }

  .social-icons a {
    width: 38px;
    height: 38px;
    border-radius: 8px;
  }

  .social-icons a svg {
    width: 18px;
    height: 18px;
  }

  .footer-bottom {
    padding: 1rem 0;
  }

  .footer-bottom p {
    font-size: 0.8rem;
    flex-wrap: wrap;
    justify-content: center;
  }

  .back-to-top {
    width: 38px;
    height: 38px;
    border-radius: 8px;
  }
}

@media (max-width: 480px) {
  .footer {
    padding: 2rem 0.75rem 0;
  }

  .footer-content {
    gap: 1.25rem;
    padding-bottom: 1.5rem;
  }

  .brand-logo {
    font-size: 1.4rem;
  }

  .brand-desc {
    font-size: 0.75rem;
  }

  .footer-links h4,
  .footer-social h4 {
    font-size: 0.85rem;
  }

  .footer-links a {
    font-size: 0.8rem;
  }

  .social-icons a {
    width: 36px;
    height: 36px;
  }

  .footer-bottom p {
    font-size: 0.75rem;
  }

  .heart-icon {
    width: 12px;
    height: 12px;
  }

  .back-to-top {
    width: 36px;
    height: 36px;
  }

  .back-to-top svg {
    width: 16px;
    height: 16px;
  }
}
</style>
