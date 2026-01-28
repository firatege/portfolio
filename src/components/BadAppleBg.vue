<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import LZString from 'lz-string'

const isPlaying = ref(false)
const currentFrame = ref('')
const showApple = ref(false)
let framesData = null
let audioPlayer = null
let scrollTimeout = null

// Debounced scroll check
function checkProjectsSection() {
  if (scrollTimeout) clearTimeout(scrollTimeout)

  scrollTimeout = setTimeout(() => {
    const projectsSection = document.getElementById('projects')
    if (projectsSection) {
      const rect = projectsSection.getBoundingClientRect()
      const windowHeight = window.innerHeight
      showApple.value = rect.top < windowHeight && rect.bottom > 0
    }
  }, 100)
}

// Load frames data
async function loadFramesData() {
  try {
    const response = await fetch('/framesData.lz')
    const data = await response.text()
    const decompressedData = LZString.decompressFromBase64(data)
    framesData = JSON.parse(decompressedData)
    console.log('Bad Apple frames loaded:', framesData.length)
  } catch (error) {
    console.error('Error loading Bad Apple frames:', error)
  }
}

// Play Bad Apple animation
function playBadApple() {
  if (!framesData || isPlaying.value) return

  isPlaying.value = true

  audioPlayer = new Audio('/bad_apple.mp3')
  audioPlayer.volume = 0.3
  audioPlayer.play()

  const fps = 30
  const frameDuration = 1000 / fps
  const startTime = performance.now()

  function renderFrame() {
    if (!isPlaying.value) return

    const elapsedTime = performance.now() - startTime
    const expectedFrame = Math.floor(elapsedTime / frameDuration)

    if (expectedFrame < framesData.length) {
      currentFrame.value = framesData[expectedFrame].replace(/\\n/g, '\n')
      requestAnimationFrame(renderFrame)
    } else {
      stopBadApple()
    }
  }

  renderFrame()
}

// Stop animation
function stopBadApple() {
  isPlaying.value = false
  currentFrame.value = ''

  if (audioPlayer) {
    audioPlayer.pause()
    audioPlayer.currentTime = 0
    audioPlayer = null
  }
}

onMounted(async () => {
  await loadFramesData()
  checkProjectsSection()
  window.addEventListener('scroll', checkProjectsSection, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', checkProjectsSection)
  if (scrollTimeout) clearTimeout(scrollTimeout)
  if (audioPlayer) {
    audioPlayer.pause()
    audioPlayer = null
  }
})
</script>

<template>
  <!-- Apple icon - fixed in top-left corner, only in projects section -->
  <Transition name="apple-fade">
    <div
      v-if="showApple && !isPlaying"
      class="apple-trigger"
      @click="playBadApple"
      title="🍎 Click to play Bad Apple"
    >
      <pre class="apple-art">
                          _/`.-'`.
                _      _/` .  _.'
       ..:::::.(_)   /` _.'_./
     .oooooooooo\ \o/.-'__.'o.
    .ooooooooo`._\_|_.'`oooooob.
  .ooooooooooooooooooooo&&oooooob.
 .oooooooooooooooooooo&@@@@@@oooob.
.ooooooooooooooooooooooo&&@@@@@ooob.
doooooooooooooooooooooooooo&@@@@ooob
doooooooooooooooooooooooooo&@@@oooob
dooooooooooooooooooooooooo&@@@ooooob
dooooooooooooooooooooooooo&@@oooooob
`dooooooooooooooooooooooooo&@ooooob'
 `doooooooooooooooooooooooooooooob'
  `doooooooooooooooooooooooooooob'
   `doooooooooooooooooooooooooob'
    `doooooooooooooooooooooooob'
     `doooooooooooooooooooooob'
      `dooooooooobodoooooooob'
       `doooooooob dooooooob'
         `"""""""' `""""""'    </pre>
    </div>
  </Transition>

  <!-- Full Bad Apple Animation Overlay -->
  <Transition name="overlay-fade">
    <div
      v-if="isPlaying"
      class="bad-apple-overlay"
      @click="stopBadApple"
    >
      <pre class="bad-apple-animation">{{ currentFrame }}</pre>
      <div class="close-hint">Click anywhere to close</div>
    </div>
  </Transition>
</template>

<style scoped>
/* Apple trigger - fixed in bottom-right corner */
.apple-trigger {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  z-index: 100;
  cursor: pointer;
  opacity: 0.08;
  transition: opacity 0.3s ease, transform 0.3s ease;
  transform: translateZ(0);
  backface-visibility: hidden;
  will-change: opacity;
}

.apple-trigger:hover {
  opacity: 0.25;
  transform: translateZ(0) scale(1.08);
}

.apple-art {
  font-family: 'Fira Code', monospace;
  font-size: 0.4rem;
  line-height: 0.5rem;
  color: #22d3ee;
  white-space: pre;
  user-select: none;
  margin: 0;
}

/* Fade transition for apple */
.apple-fade-enter-active,
.apple-fade-leave-active {
  transition: opacity 0.5s ease;
}

.apple-fade-enter-from,
.apple-fade-leave-to {
  opacity: 0;
}

/* Full screen Bad Apple overlay */
.bad-apple-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10000;
  background: rgba(0, 0, 0, 0.98);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.bad-apple-animation {
  font-family: 'Fira Code', monospace;
  font-size: clamp(0.35rem, 1.8vw, 1.2rem);
  line-height: 1.25;
  color: #22d3ee;
  white-space: pre;
  user-select: none;
  text-align: center;
}

/* Overlay fade transition */
.overlay-fade-enter-active,
.overlay-fade-leave-active {
  transition: opacity 0.3s ease;
}

.overlay-fade-enter-from,
.overlay-fade-leave-to {
  opacity: 0;
}

.close-hint {
  position: fixed;
  top: 2rem;
  left: 2rem;
  color: rgba(255, 255, 255, 0.4);
  font-size: 0.9rem;
  font-family: 'Inter', sans-serif;
}

/* Mobile Responsive */
@media (max-width: 768px) {
  .apple-trigger {
    bottom: 1.5rem;
    right: 1.5rem;
    opacity: 0.1;
  }

  .apple-art {
    font-size: 0.3rem;
    line-height: 0.4rem;
  }

  .bad-apple-animation {
    font-size: clamp(0.2rem, 1.2vw, 0.6rem);
    line-height: 1.2;
  }

  .close-hint {
    top: 1rem;
    left: 1rem;
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .apple-trigger {
    bottom: 1rem;
    right: 1rem;
    display: none; /* Hide on very small screens */
  }

  .bad-apple-animation {
    font-size: clamp(0.15rem, 1vw, 0.4rem);
    line-height: 1.15;
    padding: 0.5rem;
  }

  .close-hint {
    top: 0.75rem;
    left: 0.75rem;
    font-size: 0.7rem;
  }
}
</style>
