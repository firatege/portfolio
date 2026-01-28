<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { Menu, X } from 'lucide-vue-next'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const navLinks = [
  { name: 'About', href: '#about' },
  { name: 'Skills', href: '#skills' },
  { name: 'Experience', href: '#experience' },
  { name: 'Projects', href: '#projects' },
  { name: 'Contact', href: '#contact' }
]

function handleScroll() {
  isScrolled.value = window.scrollY > 50
}

function toggleMobileMenu() {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

function closeMobileMenu() {
  isMobileMenuOpen.value = false
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <nav class="navbar" :class="{ 'scrolled': isScrolled }">
    <div class="navbar-content">
      <!-- Logo -->
      <a href="#" class="navbar-logo">
        <span class="logo-text">FEB</span>
      </a>

      <!-- Desktop Menu -->
      <div class="navbar-menu">
        <a
          v-for="link in navLinks"
          :key="link.name"
          :href="link.href"
          class="nav-link"
        >
          {{ link.name }}
        </a>
      </div>

      <!-- Mobile Menu Button -->
      <button class="mobile-menu-btn" @click="toggleMobileMenu">
        <X v-if="isMobileMenuOpen" :size="24" />
        <Menu v-else :size="24" />
      </button>
    </div>

    <!-- Mobile Menu -->
    <Transition name="mobile-menu">
      <div v-if="isMobileMenuOpen" class="mobile-menu">
        <a
          v-for="link in navLinks"
          :key="link.name"
          :href="link.href"
          class="mobile-nav-link"
          @click="closeMobileMenu"
        >
          {{ link.name }}
        </a>
      </div>
    </Transition>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 1rem 2rem;
  transition: all 0.3s ease;
}

.navbar.scrolled {
  background: rgba(7, 13, 21, 0.9);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  padding: 0.75rem 2rem;
}

.navbar-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Logo */
.navbar-logo {
  text-decoration: none;
}

.logo-text {
  font-family: 'Fira Code', monospace;
  font-size: 1.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #22d3ee, #10b981);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  transition: all 0.3s ease;
}

.navbar-logo:hover .logo-text {
  text-shadow: 0 0 20px rgba(34, 211, 238, 0.5);
}

/* Desktop Menu */
.navbar-menu {
  display: flex;
  gap: 2rem;
}

.nav-link {
  color: rgba(255, 255, 255, 0.7);
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 500;
  position: relative;
  padding: 0.5rem 0;
  transition: color 0.2s ease;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, #22d3ee, #10b981);
  transition: width 0.3s ease;
}

.nav-link:hover {
  color: rgba(255, 255, 255, 1);
}

.nav-link:hover::after {
  width: 100%;
}

/* Mobile Menu Button */
.mobile-menu-btn {
  display: none;
  background: none;
  border: none;
  color: rgba(255, 255, 255, 0.8);
  cursor: pointer;
  padding: 0.5rem;
  transition: color 0.2s ease;
}

.mobile-menu-btn:hover {
  color: #22d3ee;
}

/* Mobile Menu */
.mobile-menu {
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: rgba(7, 13, 21, 0.98);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  padding: 1rem 2rem;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.mobile-nav-link {
  color: rgba(255, 255, 255, 0.7);
  text-decoration: none;
  font-size: 1rem;
  padding: 0.75rem 1rem;
  border-radius: 8px;
  transition: all 0.2s ease;
}

.mobile-nav-link:hover {
  background: rgba(34, 211, 238, 0.1);
  color: #22d3ee;
}

/* Mobile Menu Transition */
.mobile-menu-enter-active,
.mobile-menu-leave-active {
  transition: all 0.3s ease;
}

.mobile-menu-enter-from,
.mobile-menu-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

/* Responsive */
@media (max-width: 768px) {
  .navbar {
    padding: 0.75rem 1.25rem;
  }

  .navbar.scrolled {
    padding: 0.6rem 1.25rem;
  }

  .navbar-menu {
    display: none;
  }

  .mobile-menu-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 44px;
    height: 44px;
    border-radius: 8px;
  }

  .mobile-menu-btn:active {
    background: rgba(34, 211, 238, 0.1);
  }

  .mobile-menu {
    padding: 1rem 1.25rem 1.5rem;
  }

  .mobile-nav-link {
    font-size: 1.05rem;
    padding: 0.875rem 1rem;
    border-radius: 10px;
  }

  .logo-text {
    font-size: 1.35rem;
  }
}

@media (max-width: 480px) {
  .navbar {
    padding: 0.6rem 1rem;
  }

  .navbar.scrolled {
    padding: 0.5rem 1rem;
  }

  .logo-text {
    font-size: 1.25rem;
  }

  .mobile-menu-btn {
    width: 40px;
    height: 40px;
  }

  .mobile-menu {
    padding: 0.875rem 1rem 1.25rem;
  }

  .mobile-nav-link {
    font-size: 1rem;
    padding: 0.75rem 0.875rem;
  }
}

@media (max-width: 360px) {
  .navbar {
    padding: 0.5rem 0.75rem;
  }

  .logo-text {
    font-size: 1.15rem;
  }

  .mobile-menu-btn {
    width: 38px;
    height: 38px;
  }
}
</style>
