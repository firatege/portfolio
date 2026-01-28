<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Typing animation for roles
const roles = ['Data Scientist', 'Backend Developer', 'Computer Scientist']
const currentRole = ref(0)
const displayedText = ref('')
const isDeleting = ref(false)

// FEB/GEB Animation
const firstLetter = ref('F')
const isGlitching = ref(false)
const letterAnimated = ref([false, false, false])

let typingTimeout = null

onMounted(() => {
  // FEB letters entrance animation
  setTimeout(() => {
    [0, 1, 2].forEach((index) => {
      setTimeout(() => {
        letterAnimated.value[index] = true
      }, index * 150)
    })
  }, 300)

  // Start typing animation
  typeWriter()
})

onUnmounted(() => {
  if (typingTimeout) clearTimeout(typingTimeout)
})

function typeWriter() {
  const currentText = roles[currentRole.value]

  if (!isDeleting.value) {
    displayedText.value = currentText.substring(0, displayedText.value.length + 1)

    if (displayedText.value === currentText) {
      typingTimeout = setTimeout(() => {
        isDeleting.value = true
        typeWriter()
      }, 2500)
      return
    }
  } else {
    displayedText.value = currentText.substring(0, displayedText.value.length - 1)

    if (displayedText.value === '') {
      isDeleting.value = false
      currentRole.value = (currentRole.value + 1) % roles.length
    }
  }

  typingTimeout = setTimeout(typeWriter, isDeleting.value ? 40 : 80)
}

function triggerGlitch() {
  if (isGlitching.value) return // Prevent multiple triggers

  isGlitching.value = true

  const glitchChars = ['F', 'G', '█', '▓', '░', 'Ғ', 'Ǥ', 'ғ']
  let count = 0

  const glitchSwitch = setInterval(() => {
    // Random glitch character
    firstLetter.value = glitchChars[Math.floor(Math.random() * glitchChars.length)]
    count++


    if (count >= 12) {
      clearInterval(glitchSwitch)
      // Settle on G briefly, then back to F
      firstLetter.value = 'G'

      setTimeout(() => {
        firstLetter.value = 'F'
        setTimeout(() => {
          isGlitching.value = false
        }, 150)
      }, 400)
    }
  }, 60)
}
</script>

<template>
  <section class="hero">
    <!-- Aurora Background Effects -->
    <div class="aurora-bg">
      <div class="aurora aurora-1"></div>
      <div class="aurora aurora-2"></div>
      <div class="aurora aurora-3"></div>
    </div>

    <!-- Floating Particles -->
    <div class="particles">
      <div class="particle" v-for="n in 20" :key="n"></div>
    </div>

    <div class="hero-content" :class="{ 'page-glitch': isGlitching }">
      <!-- FEB/GEB Animation -->
      <div class="feb-container">
        <div class="feb-wrapper">
          <span
            class="feb-letter first-letter"
            :class="{ 'animated': letterAnimated[0], 'glitching': isGlitching }"
            @click="triggerGlitch"
          >
            {{ firstLetter }}
            <span class="glitch-layer glitch-1" v-if="isGlitching">{{ firstLetter }}</span>
            <span class="glitch-layer glitch-2" v-if="isGlitching">{{ firstLetter }}</span>
          </span>
          <span
            class="feb-letter other-letter"
            :class="{ 'animated': letterAnimated[1], 'glitch-shake': isGlitching }"
          >
            E
          </span>
          <span
            class="feb-letter other-letter"
            :class="{ 'animated': letterAnimated[2], 'glitch-shake': isGlitching }"
          >
            B
          </span>
        </div>
        <div class="feb-underline" :class="{ 'line-glitch': isGlitching }"></div>
      </div>

      <!-- Main Name -->
      <h1 class="name" :class="{ 'red-glitch': isGlitching }">FIRAT EGE</h1>

      <!-- Typing Role Animation -->
      <div class="role-container" :class="{ 'red-glitch': isGlitching }">
        <span class="role-bracket">&lt;</span>
        <span class="role-text">{{ displayedText }}</span>
        <span class="cursor">|</span>
        <span class="role-bracket">/&gt;</span>
      </div>

      <!-- Short About -->
      <p class="tagline" :class="{ 'text-glitch': isGlitching }">
        Building data-driven systems & scalable architectures
      </p>

      <!-- CTA Buttons -->
      <div class="cta-buttons" :class="{ 'elements-glitch': isGlitching }">
        <a href="#about" class="btn btn-primary">
          <span>About Me</span>
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 5v14M19 12l-7 7-7-7"/>
          </svg>
        </a>
        <a href="#projects" class="btn btn-secondary">
          <span>View Projects</span>
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M5 12h14M12 5l7 7-7 7"/>
          </svg>
        </a>
      </div>

      <!-- Social Links -->
      <div class="social-links" :class="{ 'elements-glitch': isGlitching }">
        <a href="https://github.com/firatege" target="_blank" class="social-link" title="GitHub">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
          </svg>
        </a>
        <a href="https://www.linkedin.com/in/byfeb" target="_blank" class="social-link" title="LinkedIn">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
            <path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/>
          </svg>
        </a>
        <a href="https://x.com/FratEgeBayram1" target="_blank" class="social-link" title="X (Twitter)">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
            <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
          </svg>
        </a>
        <a href="mailto:firategebayram@gmail.com" class="social-link" title="Email">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
            <polyline points="22,6 12,13 2,6"/>
          </svg>
        </a>
      </div>
    </div>

    <!-- Scroll Indicator -->
    <div class="scroll-indicator" :class="{ 'elements-glitch': isGlitching }">
      <div class="mouse">
        <div class="wheel"></div>
      </div>
      <span>Scroll Down</span>
    </div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  padding: 2rem;
  background: radial-gradient(ellipse at 50% 50%, #0c1929 0%, #070d15 100%);
}

/* Aurora Background - Only top and middle of Hero */
.aurora-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 70%; /* Only covers top 70% of hero */
  overflow: visible;
  z-index: 0;
  pointer-events: none;
}

.aurora {
  position: absolute;
  border-radius: 50%;
  filter: blur(100px);
  opacity: 0.4;
  mix-blend-mode: screen;
}

/* Aurora 1 - Top left */
.aurora-1 {
  width: 80vw;
  height: 80vw;
  max-width: 800px;
  max-height: 800px;
  background: radial-gradient(circle, rgba(14, 165, 233, 0.6) 0%, rgba(6, 182, 212, 0.3) 40%, transparent 70%);
  top: -30%;
  left: -15%;
  animation: aurora1Move 20s ease-in-out infinite;
}

/* Aurora 2 - Top right */
.aurora-2 {
  width: 70vw;
  height: 70vw;
  max-width: 700px;
  max-height: 700px;
  background: radial-gradient(circle, rgba(16, 185, 129, 0.5) 0%, rgba(52, 211, 153, 0.2) 40%, transparent 70%);
  top: -10%;
  right: -20%;
  animation: aurora2Move 25s ease-in-out infinite;
}

/* Aurora 3 - Center/middle area */
.aurora-3 {
  width: 60vw;
  height: 60vw;
  max-width: 600px;
  max-height: 600px;
  background: radial-gradient(circle, rgba(8, 145, 178, 0.4) 0%, rgba(34, 211, 238, 0.15) 40%, transparent 70%);
  top: 20%;
  left: 30%;
  animation: aurora3Move 22s ease-in-out infinite;
}

@keyframes aurora1Move {
  0%, 100% {
    transform: translate(0, 0) scale(1);
    opacity: 0.4;
  }
  33% {
    transform: translate(50px, 30px) scale(1.1);
    opacity: 0.5;
  }
  66% {
    transform: translate(-30px, -20px) scale(0.95);
    opacity: 0.35;
  }
}

@keyframes aurora2Move {
  0%, 100% {
    transform: translate(0, 0) scale(1);
    opacity: 0.4;
  }
  33% {
    transform: translate(-40px, 40px) scale(1.05);
    opacity: 0.45;
  }
  66% {
    transform: translate(30px, -30px) scale(0.9);
    opacity: 0.35;
  }
}

@keyframes aurora3Move {
  0%, 100% {
    transform: translate(0, 0) scale(1);
    opacity: 0.4;
  }
  33% {
    transform: translate(30px, -30px) scale(1.08);
    opacity: 0.5;
  }
  66% {
    transform: translate(-40px, 20px) scale(0.92);
    opacity: 0.3;
  }
}

/* Particles - Smaller and more subtle */
.particles {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.particle {
  position: absolute;
  width: 3px;
  height: 3px;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 50%;
  animation: twinkle 5s ease-in-out infinite;
  box-shadow: 0 0 6px rgba(255, 255, 255, 0.3);
}

.particle:nth-child(1) { top: 10%; left: 20%; animation-delay: 0s; }
.particle:nth-child(2) { top: 20%; left: 80%; animation-delay: 0.5s; }
.particle:nth-child(3) { top: 30%; left: 10%; animation-delay: 1s; }
.particle:nth-child(4) { top: 40%; left: 60%; animation-delay: 1.5s; }
.particle:nth-child(5) { top: 50%; left: 30%; animation-delay: 2s; }
.particle:nth-child(6) { top: 60%; left: 90%; animation-delay: 2.5s; }
.particle:nth-child(7) { top: 70%; left: 15%; animation-delay: 3s; }
.particle:nth-child(8) { top: 80%; left: 70%; animation-delay: 3.5s; }
.particle:nth-child(9) { top: 15%; left: 45%; animation-delay: 0.3s; }
.particle:nth-child(10) { top: 25%; left: 55%; animation-delay: 0.8s; }
.particle:nth-child(11) { top: 35%; left: 85%; animation-delay: 1.3s; }
.particle:nth-child(12) { top: 45%; left: 5%; animation-delay: 1.8s; }
.particle:nth-child(13) { top: 55%; left: 75%; animation-delay: 2.3s; }
.particle:nth-child(14) { top: 65%; left: 25%; animation-delay: 2.8s; }
.particle:nth-child(15) { top: 75%; left: 95%; animation-delay: 3.3s; }
.particle:nth-child(16) { top: 85%; left: 40%; animation-delay: 0.1s; }
.particle:nth-child(17) { top: 90%; left: 65%; animation-delay: 0.6s; }
.particle:nth-child(18) { top: 5%; left: 35%; animation-delay: 1.1s; }
.particle:nth-child(19) { top: 95%; left: 50%; animation-delay: 1.6s; }
.particle:nth-child(20) { top: 12%; left: 92%; animation-delay: 2.1s; }

@keyframes twinkle {
  0%, 100% {
    opacity: 0.3;
    transform: scale(1);
  }
  50% {
    opacity: 1;
    transform: scale(1.5);
  }
}

/* Hero Content */
.hero-content {
  text-align: center;
  z-index: 2;
  position: relative;
}

/* FEB Animation - Enhanced */
.feb-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 1rem;
  position: relative;
  padding: 1rem 2rem;
}

/* Red Glitch Effect for text */
.red-glitch {
  animation: redGlitchText 0.1s linear infinite;
  position: relative;
}

.red-glitch::before,
.red-glitch::after {
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

@keyframes redGlitchText {
  0% {
    color: #ff0000;
    text-shadow: 2px 0 #00ffff, -2px 0 #ff00ff;
    transform: translate(0);
  }
  20% {
    color: #ff3333;
    text-shadow: -3px 0 #00ffff, 3px 0 #ff00ff;
    transform: translate(-2px, 1px);
  }
  40% {
    color: #ff0000;
    text-shadow: 3px 0 #00ffff, -3px 0 #ff00ff;
    transform: translate(2px, -1px);
  }
  60% {
    color: #ff4444;
    text-shadow: -2px 0 #00ffff, 2px 0 #ff00ff;
    transform: translate(-1px, 2px);
  }
  80% {
    color: #ff0000;
    text-shadow: 2px 0 #00ffff, -2px 0 #ff00ff;
    transform: translate(1px, -2px);
  }
  100% {
    color: #ff2222;
    text-shadow: -3px 0 #00ffff, 3px 0 #ff00ff;
    transform: translate(0);
  }
}

.feb-wrapper {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
}

.feb-letter {
  font-size: clamp(4rem, 12vw, 8rem);
  font-weight: 900;
  color: transparent;
  background: linear-gradient(135deg, #06b6d4, #10b981, #0ea5e9);
  background-size: 200% 200%;
  -webkit-background-clip: text;
  background-clip: text;
  opacity: 0;
  transform: translateY(50px) scale(0.5);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  animation: gradientShift 4s ease-in-out infinite;
  position: relative;
  display: inline-block;
}

.feb-letter.animated {
  opacity: 1;
  transform: translateY(0) scale(1);
}

/* Only F letter has hover effect and is clickable */
.first-letter {
  cursor: pointer;
  transition: all 0.3s ease;
}

.first-letter:hover {
  transform: scale(1.15) translateY(-8px);
  filter: drop-shadow(0 0 40px rgba(6, 182, 212, 0.9)) drop-shadow(0 0 80px rgba(16, 185, 129, 0.5));
}

/* E and B letters - no hover effect */
.other-letter {
  cursor: default;
}

/* Glitch Layers */
.first-letter {
  position: relative;
}

.glitch-layer {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #06b6d4, #10b981);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.glitch-1 {
  animation: glitch1 0.1s infinite;
  text-shadow: 2px 0 #ff0080;
  clip-path: polygon(0 0, 100% 0, 100% 45%, 0 45%);
}

.glitch-2 {
  animation: glitch2 0.1s infinite;
  text-shadow: -2px 0 #00ff80;
  clip-path: polygon(0 55%, 100% 55%, 100% 100%, 0 100%);
}

@keyframes glitch1 {
  0%, 100% { transform: translate(0); }
  20% { transform: translate(-3px, 2px); }
  40% { transform: translate(3px, -2px); }
  60% { transform: translate(-2px, -1px); }
  80% { transform: translate(2px, 1px); }
}

@keyframes glitch2 {
  0%, 100% { transform: translate(0); }
  20% { transform: translate(3px, -2px); }
  40% { transform: translate(-3px, 2px); }
  60% { transform: translate(2px, 1px); }
  80% { transform: translate(-2px, -1px); }
}

/* Glitch Effect for F/G */
.first-letter.glitching {
  animation: mainGlitch 0.08s ease-in-out infinite;
}

.glitch-shake {
  animation: shake 0.1s ease-in-out infinite;
}

@keyframes mainGlitch {
  0%, 100% {
    transform: translate(0) skew(0deg);
    filter: hue-rotate(0deg);
  }
  25% {
    transform: translate(-4px, 2px) skew(2deg);
    filter: hue-rotate(90deg);
  }
  50% {
    transform: translate(4px, -2px) skew(-2deg);
    filter: hue-rotate(180deg);
  }
  75% {
    transform: translate(-2px, -1px) skew(1deg);
    filter: hue-rotate(270deg);
  }
}

@keyframes shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-2px); }
  75% { transform: translateX(2px); }
}

@keyframes gradientShift {
  0%, 100% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
}

.feb-underline {
  width: 0;
  height: 4px;
  background: linear-gradient(90deg, #06b6d4, #10b981);
  border-radius: 2px;
  margin-top: 0.5rem;
  animation: underlineExpand 1s ease-out 0.8s forwards;
}

@keyframes underlineExpand {
  to {
    width: 100%;
  }
}

/* ============================================
   PAGE-WIDE GLITCH EFFECTS
   ============================================ */

/* Main content glitch */
.page-glitch {
  animation: pageShake 0.1s ease-in-out infinite;
}

@keyframes pageShake {
  0%, 100% { transform: translate(0); }
  10% { transform: translate(-2px, 1px); }
  30% { transform: translate(2px, -1px); }
  50% { transform: translate(-1px, -1px); }
  70% { transform: translate(1px, 2px); }
  90% { transform: translate(-1px, 1px); }
}

/* Text elements glitch - red/cyan chromatic aberration */
.text-glitch {
  animation: textGlitch 0.15s ease-in-out infinite;
  position: relative;
}

@keyframes textGlitch {
  0%, 100% {
    text-shadow: none;
    transform: translate(0);
  }
  20% {
    text-shadow: -2px 0 #ff0040, 2px 0 #00ffff;
    transform: translate(-1px, 1px);
  }
  40% {
    text-shadow: 2px 0 #ff0040, -2px 0 #00ffff;
    transform: translate(1px, -1px);
  }
  60% {
    text-shadow: -1px 0 #ff0040, 1px 0 #00ffff;
    transform: translate(1px, 1px);
  }
  80% {
    text-shadow: 1px 0 #ff0040, -1px 0 #00ffff;
    transform: translate(-1px, -1px);
  }
}

/* Underline glitch */
.line-glitch {
  animation: lineGlitch 0.1s ease-in-out infinite;
}

@keyframes lineGlitch {
  0%, 100% {
    transform: scaleX(1) translateX(0);
    opacity: 1;
  }
  25% {
    transform: scaleX(0.8) translateX(-10px);
    opacity: 0.7;
    background: linear-gradient(90deg, #ff0040, #00ffff);
  }
  50% {
    transform: scaleX(1.1) translateX(5px);
    opacity: 0.9;
  }
  75% {
    transform: scaleX(0.9) translateX(-5px);
    opacity: 0.6;
    background: linear-gradient(90deg, #00ffff, #ff0040);
  }
}

/* Buttons and icons glitch */
.elements-glitch {
  animation: elementsGlitch 0.12s ease-in-out infinite;
}

@keyframes elementsGlitch {
  0%, 100% {
    filter: none;
    transform: translate(0);
  }
  20% {
    filter: hue-rotate(90deg) saturate(2);
    transform: translate(-3px, 1px) skewX(2deg);
  }
  40% {
    filter: hue-rotate(180deg) brightness(1.2);
    transform: translate(2px, -2px) skewX(-1deg);
  }
  60% {
    filter: hue-rotate(270deg) saturate(1.5);
    transform: translate(-1px, 2px) skewX(1deg);
  }
  80% {
    filter: hue-rotate(45deg) contrast(1.2);
    transform: translate(1px, -1px) skewX(-2deg);
  }
}

/* ============================================
   END GLITCH EFFECTS
   ============================================ */

/* Name */
.name {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  font-weight: 300;
  letter-spacing: 0.4em;
  color: rgba(255, 255, 255, 0.85);
  margin-bottom: 2rem;
  animation: fadeInUp 1s ease-out 0.5s both;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Role Typing Animation */
.role-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  font-size: clamp(1.2rem, 3vw, 1.6rem);
  margin-bottom: 2rem;
  font-family: 'Fira Code', 'Consolas', monospace;
  animation: fadeInUp 1s ease-out 0.7s both;
}

.role-bracket {
  color: rgba(255, 255, 255, 0.4);
  font-weight: 300;
}

.role-text {
  color: #22d3ee;
  font-weight: 500;
  min-width: 200px;
  text-align: left;
}

.cursor {
  color: #10b981;
  font-weight: 300;
  animation: blink 0.8s infinite;
}

@keyframes blink {
  0%, 50% { opacity: 1; }
  51%, 100% { opacity: 0; }
}

/* Tagline */
.tagline {
  font-size: clamp(1rem, 2vw, 1.2rem);
  color: rgba(255, 255, 255, 0.6);
  max-width: 500px;
  margin: 0 auto 2.5rem;
  animation: fadeInUp 1s ease-out 0.9s both;
}

/* CTA Buttons */
.cta-buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 2.5rem;
  animation: fadeInUp 1s ease-out 1.1s both;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.875rem 1.75rem;
  border-radius: 50px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
  cursor: pointer;
}

.btn-primary {
  background: linear-gradient(135deg, #0ea5e9, #10b981);
  color: white;
  box-shadow: 0 4px 20px rgba(14, 165, 233, 0.4);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 30px rgba(14, 165, 233, 0.6);
}

.btn-secondary {
  background: transparent;
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
}

.btn-secondary:hover {
  border-color: #10b981;
  background: rgba(16, 185, 129, 0.1);
  transform: translateY(-3px);
}

/* Social Links */
.social-links {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  animation: fadeInUp 1s ease-out 1.3s both;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  color: rgba(255, 255, 255, 0.8);
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.social-link:hover {
  background: linear-gradient(135deg, #0ea5e9, #10b981);
  color: white;
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(14, 165, 233, 0.4);
}

/* Scroll Indicator - Centered */
.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 0;
  right: 0;
  margin: 0 auto;
  width: fit-content;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  color: rgba(255, 255, 255, 0.5);
  font-size: 0.875rem;
  animation: fadeInUp 1s ease-out 1.5s both;
  z-index: 2;
}

.mouse {
  width: 24px;
  height: 40px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 12px;
  position: relative;
}

.wheel {
  width: 4px;
  height: 8px;
  background: #10b981;
  border-radius: 2px;
  position: absolute;
  top: 8px;
  left: 50%;
  transform: translateX(-50%);
  animation: scroll 2s ease-in-out infinite;
}

@keyframes scroll {
  0%, 100% {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
  50% {
    opacity: 0.5;
    transform: translateX(-50%) translateY(10px);
  }
}

/* Responsive */
@media (max-width: 768px) {
  .hero {
    padding: 1.5rem;
    padding-top: 80px;
  }

  .feb-letter {
    font-size: clamp(3rem, 15vw, 5rem);
  }

  .role-text {
    min-width: 150px;
  }

  .cta-buttons {
    flex-direction: column;
    align-items: center;
    width: 100%;
    padding: 0 1rem;
  }

  .btn {
    width: 100%;
    max-width: 280px;
    justify-content: center;
  }

  .social-links {
    gap: 1rem;
  }

  .social-link {
    width: 44px;
    height: 44px;
  }

  .scroll-indicator {
    bottom: 1.5rem;
  }

  .scroll-indicator span {
    font-size: 0.75rem;
  }

  .aurora-1 {
    width: 100vw;
    height: 100vw;
    max-width: 400px;
    max-height: 400px;
    top: -20%;
    left: -30%;
  }

  .aurora-2 {
    width: 90vw;
    height: 90vw;
    max-width: 350px;
    max-height: 350px;
    top: -5%;
    right: -30%;
  }

  .aurora-3 {
    width: 80vw;
    height: 80vw;
    max-width: 300px;
    max-height: 300px;
    top: 30%;
    left: 20%;
  }
}

@media (max-width: 480px) {
  .hero {
    padding: 1rem;
    padding-top: 70px;
  }

  .feb-letter {
    font-size: clamp(2.5rem, 12vw, 4rem);
  }

  .feb-wrapper {
    gap: 0.3rem;
  }

  .name {
    font-size: clamp(1.2rem, 5vw, 1.5rem);
    letter-spacing: 0.2em;
  }

  .role-container {
    font-size: clamp(0.9rem, 3vw, 1.1rem);
    gap: 0.3rem;
    flex-wrap: wrap;
    justify-content: center;
    padding: 0 0.5rem;
  }

  .role-text {
    min-width: 120px;
    text-align: center;
  }

  .tagline {
    font-size: 0.9rem;
    padding: 0 0.5rem;
    margin-bottom: 2rem;
  }

  .btn {
    padding: 0.75rem 1.5rem;
    font-size: 0.9rem;
  }

  .social-link {
    width: 42px;
    height: 42px;
  }

  .social-link svg {
    width: 20px;
    height: 20px;
  }

  .particles {
    display: none;
  }
}

@media (max-width: 360px) {
  .feb-letter {
    font-size: clamp(2rem, 10vw, 3rem);
  }

  .role-container {
    font-size: 0.85rem;
  }

  .btn {
    max-width: 100%;
    padding: 0.7rem 1.25rem;
    font-size: 0.85rem;
  }
}
</style>
