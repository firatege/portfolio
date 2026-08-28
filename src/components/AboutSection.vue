<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)
const statsAnimated = ref(false)

// Stats data
const stats = [
  { number: '3.0', label: 'GPA' },
  { number: '3+', label: 'Years Coding' },
  { number: '10+', label: 'Projects' },
  { number: '5+', label: 'Technologies' }
]

// Academic courses with icon names (will use SVG)
const courses = [
  { icon: 'database', title: 'Data Mining', desc: 'Pattern recognition & knowledge discovery from large datasets' },
  { icon: 'chart', title: 'Multivariate Data Analysis', desc: 'Statistical analysis of multi-dimensional data' },
  { icon: 'math', title: 'Mathematical Programming', desc: 'Optimization techniques & linear programming' },
  { icon: 'brain', title: 'Fuzzy Logic', desc: 'Handling uncertainty in computational systems' },
  { icon: 'globe', title: 'Web & Data Mining', desc: 'Extracting insights from web data sources' },
  { icon: 'trending', title: 'Basic Statistics', desc: 'Foundation of statistical inference & probability' }
]

onMounted(() => {
  // Intersection Observer for scroll animations
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true
          setTimeout(() => {
            statsAnimated.value = true
          }, 500)
        }
      })
    },
    { threshold: 0.2 }
  )

  const section = document.querySelector('.about-section')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="about" class="about-section">
    <!-- Stars/particles only - aurora comes from Hero section -->
    <div class="stars-container">
      <div class="star" v-for="n in 50" :key="n"></div>
    </div>

    <!-- Ambient particles -->
    <div class="ambient-particles">
      <div class="ambient-particle" v-for="n in 15" :key="n"></div>
    </div>

    <div class="about-container" :class="{ 'visible': isVisible }">
      <!-- Section Header -->
      <div class="section-header">
        <span class="section-tag">&lt;about&gt;</span>
        <h2 class="section-title">About Me</h2>
        <div class="title-underline"></div>
      </div>

      <!-- Main Content Grid -->
      <div class="about-grid">
        <!-- Left: Photo & Quick Info -->
        <div class="about-left">
          <div class="photo-container">
            <div class="photo-frame"></div>
            <div class="photo-glow"></div>
          </div>

          <!-- Quick Stats -->
          <div class="stats-grid" :class="{ 'animated': statsAnimated }">
            <div class="stat-item" v-for="(stat, index) in stats" :key="index" :style="{ animationDelay: `${index * 0.1}s` }">
              <span class="stat-number">{{ stat.number }}</span>
              <span class="stat-label">{{ stat.label }}</span>
            </div>
          </div>
        </div>

        <!-- Right: About Text -->
        <div class="about-right">
          <div class="about-text">
            <p class="intro-text">
              Hi! I'm <span class="highlight">Fırat Ege</span>, but you can call me <span class="highlight-alt">FEB</span>.
            </p>

            <p>
              I'm a Computer Science student at <span class="highlight">Dokuz Eylül University</span>,
              focused on building <span class="highlight-alt">data-driven systems</span>,
              <span class="highlight-alt">AI applications</span>, and
              <span class="highlight-alt">scalable backend architectures</span>.
            </p>

            <p>
              I believe in crafting technical solutions that are not just functional, but
              <strong>sustainable</strong>, <strong>readable</strong>, and <strong>contextually meaningful</strong>.
              I bridge the gap between academic knowledge and practical engineering.
            </p>

            <p>
              Currently exploring the intersection of <span class="highlight">Machine Learning</span>,
              <span class="highlight">NLP</span>, and <span class="highlight">Backend Development</span> —
              building systems that actually solve real-world problems.
            </p>
          </div>

          <!-- Education Badge - Below about text, slightly centered -->
          <div class="education-badge">
            <div class="edu-icon-wrapper">
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <path d="M22 10v6M2 10l10-5 10 5-10 5z"/>
                <path d="M6 12v5c3 3 9 3 12 0v-5"/>
              </svg>
            </div>
            <div class="edu-info">
              <span class="edu-school">Dokuz Eylül University</span>
              <span class="edu-degree">B.Sc. Computer Science</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Academic Background Section -->
      <div class="academic-section">
        <h3 class="academic-title">Academic Background</h3>
        <p class="academic-subtitle">Relevant coursework that shaped my technical foundation</p>
        <div class="courses-grid">
          <div
            class="course-card"
            v-for="(course, index) in courses"
            :key="index"
            :style="{ animationDelay: `${index * 0.1}s` }"
          >
            <div class="course-icon">
              <!-- Database icon -->
              <svg v-if="course.icon === 'database'" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <ellipse cx="12" cy="5" rx="9" ry="3"/>
                <path d="M21 12c0 1.66-4 3-9 3s-9-1.34-9-3"/>
                <path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"/>
              </svg>
              <!-- Chart icon -->
              <svg v-if="course.icon === 'chart'" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <line x1="18" y1="20" x2="18" y2="10"/>
                <line x1="12" y1="20" x2="12" y2="4"/>
                <line x1="6" y1="20" x2="6" y2="14"/>
                <line x1="3" y1="20" x2="21" y2="20"/>
              </svg>
              <!-- Math icon -->
              <svg v-if="course.icon === 'math'" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <line x1="4" y1="9" x2="20" y2="9"/>
                <line x1="4" y1="15" x2="20" y2="15"/>
                <line x1="10" y1="3" x2="8" y2="21"/>
                <line x1="16" y1="3" x2="14" y2="21"/>
              </svg>
              <!-- Brain icon -->
              <svg v-if="course.icon === 'brain'" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <path d="M9.5 2A2.5 2.5 0 0 1 12 4.5v15a2.5 2.5 0 0 1-4.96.44 2.5 2.5 0 0 1-2.96-3.08 3 3 0 0 1-.34-5.58 2.5 2.5 0 0 1 1.32-4.24 2.5 2.5 0 0 1 4.44-1.54"/>
                <path d="M14.5 2A2.5 2.5 0 0 0 12 4.5v15a2.5 2.5 0 0 0 4.96.44 2.5 2.5 0 0 0 2.96-3.08 3 3 0 0 0 .34-5.58 2.5 2.5 0 0 0-1.32-4.24 2.5 2.5 0 0 0-4.44-1.54"/>
              </svg>
              <!-- Globe icon -->
              <svg v-if="course.icon === 'globe'" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <circle cx="12" cy="12" r="10"/>
                <line x1="2" y1="12" x2="22" y2="12"/>
                <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>
              </svg>
              <!-- Trending icon -->
              <svg v-if="course.icon === 'trending'" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <polyline points="23 6 13.5 15.5 8.5 10.5 1 18"/>
                <polyline points="17 6 23 6 23 12"/>
              </svg>
            </div>
            <h4 class="course-title">{{ course.title }}</h4>
            <p class="course-desc">{{ course.desc }}</p>
          </div>
        </div>
      </div>

      <!-- Section Close Tag -->
      <div class="section-footer">
        <span class="section-tag">&lt;/about&gt;</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-section {
  min-height: 100vh;
  padding: 6rem 2rem;
  position: relative;
  overflow: hidden;
  /* Same background as Hero */
  background: radial-gradient(ellipse at 50% 50%, #0c1929 0%, #070d15 100%);
}

/* Stars Background */
.stars-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: 0;
  pointer-events: none;
}

.star {
  position: absolute;
  width: 2px;
  height: 2px;
  background: white;
  border-radius: 50%;
  opacity: 0;
  animation: twinkleStar 4s ease-in-out infinite;
}

/* Distribute stars randomly */
.star:nth-child(1) { top: 5%; left: 10%; animation-delay: 0s; }
.star:nth-child(2) { top: 8%; left: 25%; animation-delay: 0.5s; }
.star:nth-child(3) { top: 12%; left: 45%; animation-delay: 1s; }
.star:nth-child(4) { top: 6%; left: 60%; animation-delay: 1.5s; }
.star:nth-child(5) { top: 15%; left: 80%; animation-delay: 2s; }
.star:nth-child(6) { top: 20%; left: 15%; animation-delay: 0.3s; }
.star:nth-child(7) { top: 25%; left: 35%; animation-delay: 0.8s; }
.star:nth-child(8) { top: 22%; left: 55%; animation-delay: 1.3s; }
.star:nth-child(9) { top: 18%; left: 75%; animation-delay: 1.8s; }
.star:nth-child(10) { top: 28%; left: 90%; animation-delay: 2.3s; }
.star:nth-child(11) { top: 32%; left: 5%; animation-delay: 0.1s; }
.star:nth-child(12) { top: 35%; left: 22%; animation-delay: 0.6s; }
.star:nth-child(13) { top: 38%; left: 42%; animation-delay: 1.1s; }
.star:nth-child(14) { top: 33%; left: 65%; animation-delay: 1.6s; }
.star:nth-child(15) { top: 40%; left: 85%; animation-delay: 2.1s; }
.star:nth-child(16) { top: 45%; left: 12%; animation-delay: 0.4s; }
.star:nth-child(17) { top: 48%; left: 30%; animation-delay: 0.9s; }
.star:nth-child(18) { top: 52%; left: 50%; animation-delay: 1.4s; }
.star:nth-child(19) { top: 47%; left: 70%; animation-delay: 1.9s; }
.star:nth-child(20) { top: 55%; left: 88%; animation-delay: 2.4s; }
.star:nth-child(21) { top: 58%; left: 8%; animation-delay: 0.2s; }
.star:nth-child(22) { top: 62%; left: 28%; animation-delay: 0.7s; }
.star:nth-child(23) { top: 65%; left: 48%; animation-delay: 1.2s; }
.star:nth-child(24) { top: 60%; left: 68%; animation-delay: 1.7s; }
.star:nth-child(25) { top: 68%; left: 92%; animation-delay: 2.2s; }
.star:nth-child(26) { top: 72%; left: 18%; animation-delay: 0.15s; }
.star:nth-child(27) { top: 75%; left: 38%; animation-delay: 0.65s; }
.star:nth-child(28) { top: 78%; left: 58%; animation-delay: 1.15s; }
.star:nth-child(29) { top: 73%; left: 78%; animation-delay: 1.65s; }
.star:nth-child(30) { top: 80%; left: 95%; animation-delay: 2.15s; }
.star:nth-child(31) { top: 82%; left: 3%; animation-delay: 0.25s; }
.star:nth-child(32) { top: 85%; left: 20%; animation-delay: 0.75s; }
.star:nth-child(33) { top: 88%; left: 40%; animation-delay: 1.25s; }
.star:nth-child(34) { top: 83%; left: 62%; animation-delay: 1.75s; }
.star:nth-child(35) { top: 90%; left: 82%; animation-delay: 2.25s; }
.star:nth-child(36) { top: 92%; left: 10%; animation-delay: 0.35s; }
.star:nth-child(37) { top: 95%; left: 32%; animation-delay: 0.85s; }
.star:nth-child(38) { top: 93%; left: 52%; animation-delay: 1.35s; }
.star:nth-child(39) { top: 97%; left: 72%; animation-delay: 1.85s; }
.star:nth-child(40) { top: 94%; left: 90%; animation-delay: 2.35s; }
.star:nth-child(41) { top: 10%; left: 5%; animation-delay: 2.5s; }
.star:nth-child(42) { top: 30%; left: 95%; animation-delay: 2.6s; }
.star:nth-child(43) { top: 50%; left: 3%; animation-delay: 2.7s; }
.star:nth-child(44) { top: 70%; left: 97%; animation-delay: 2.8s; }
.star:nth-child(45) { top: 15%; left: 50%; animation-delay: 2.9s; }
.star:nth-child(46) { top: 42%; left: 25%; animation-delay: 3s; }
.star:nth-child(47) { top: 67%; left: 75%; animation-delay: 3.1s; }
.star:nth-child(48) { top: 88%; left: 15%; animation-delay: 3.2s; }
.star:nth-child(49) { top: 25%; left: 85%; animation-delay: 3.3s; }
.star:nth-child(50) { top: 55%; left: 35%; animation-delay: 3.4s; }

@keyframes twinkleStar {
  0%, 100% {
    opacity: 0.2;
    transform: scale(1);
  }
  50% {
    opacity: 0.8;
    transform: scale(1.2);
  }
}

/* Ambient particles - different animation than hero */
.ambient-particles {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1;
  overflow: hidden;
}

.ambient-particle {
  position: absolute;
  width: 3px;
  height: 3px;
  background: rgba(16, 185, 129, 0.5);
  border-radius: 50%;
  animation: floatHorizontal 25s linear infinite;
  box-shadow: 0 0 8px rgba(16, 185, 129, 0.3);
}

.ambient-particle:nth-child(odd) {
  background: rgba(34, 211, 238, 0.4);
  box-shadow: 0 0 8px rgba(34, 211, 238, 0.3);
}

.ambient-particle:nth-child(1) { top: 5%; animation-delay: 0s; animation-duration: 20s; }
.ambient-particle:nth-child(2) { top: 12%; animation-delay: 2s; animation-duration: 25s; }
.ambient-particle:nth-child(3) { top: 20%; animation-delay: 4s; animation-duration: 22s; }
.ambient-particle:nth-child(4) { top: 28%; animation-delay: 1s; animation-duration: 28s; }
.ambient-particle:nth-child(5) { top: 35%; animation-delay: 3s; animation-duration: 24s; }
.ambient-particle:nth-child(6) { top: 45%; animation-delay: 5s; animation-duration: 26s; }
.ambient-particle:nth-child(7) { top: 55%; animation-delay: 2.5s; animation-duration: 21s; }
.ambient-particle:nth-child(8) { top: 65%; animation-delay: 4.5s; animation-duration: 27s; }
.ambient-particle:nth-child(9) { top: 75%; animation-delay: 1.5s; animation-duration: 23s; }
.ambient-particle:nth-child(10) { top: 85%; animation-delay: 3.5s; animation-duration: 29s; }
.ambient-particle:nth-child(11) { top: 92%; animation-delay: 6s; animation-duration: 20s; }
.ambient-particle:nth-child(12) { top: 18%; animation-delay: 7s; animation-duration: 25s; }
.ambient-particle:nth-child(13) { top: 40%; animation-delay: 8s; animation-duration: 22s; }
.ambient-particle:nth-child(14) { top: 60%; animation-delay: 9s; animation-duration: 28s; }
.ambient-particle:nth-child(15) { top: 80%; animation-delay: 10s; animation-duration: 24s; }

/* Horizontal floating animation - different from hero's vertical */
@keyframes floatHorizontal {
  0% {
    left: -5%;
    opacity: 0;
    transform: scale(0);
  }
  5% {
    opacity: 1;
    transform: scale(1);
  }
  95% {
    opacity: 1;
    transform: scale(1);
  }
  100% {
    left: 105%;
    opacity: 0;
    transform: scale(0);
  }
}

/* Container */
.about-container {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 2;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease-out;
}

.about-container.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Section Header */
.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-tag {
  font-family: 'Fira Code', monospace;
  color: rgba(34, 211, 238, 0.6);
  font-size: 1rem;
  letter-spacing: 0.1em;
}

.section-title {
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  background: linear-gradient(135deg, #22d3ee, #10b981);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  margin: 0.5rem 0 1rem;
}

.title-underline {
  width: 100px;
  height: 4px;
  background: linear-gradient(90deg, #06b6d4, #10b981);
  margin: 0 auto;
  border-radius: 2px;
}

/* Main Grid */
.about-grid {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 4rem;
  margin-bottom: 4rem;
}

/* Left Column - Photo */
.about-left {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.photo-container {
  position: relative;
  display: flex;
  justify-content: center;
}

.photo-frame {
  width: 280px;
  height: 320px;
  border-radius: 20px;
  overflow: hidden;
  position: relative;
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.2), rgba(16, 185, 129, 0.2));
  border: 2px solid rgba(255, 255, 255, 0.1);
  z-index: 2;
}

.profile-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.photo-frame:hover .profile-photo {
  transform: scale(1.05);
}

.photo-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 300px;
  height: 340px;
  background: radial-gradient(circle, rgba(6, 182, 212, 0.3) 0%, transparent 70%);
  filter: blur(40px);
  z-index: 1;
}

/* Stats Grid */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}

.stat-item {
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 12px;
  padding: 1.25rem;
  text-align: center;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.4s ease;
}

.stats-grid.animated .stat-item {
  opacity: 1;
  transform: translateY(0);
  animation: statPop 0.5s ease-out forwards;
}

@keyframes statPop {
  0% {
    opacity: 0;
    transform: translateY(20px) scale(0.9);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.stat-item:hover {
  background: rgba(255, 255, 255, 0.06);
  border-color: rgba(34, 211, 238, 0.3);
  transform: translateY(-5px);
}

.stat-number {
  display: block;
  font-size: 2rem;
  font-weight: 800;
  background: linear-gradient(135deg, #22d3ee, #10b981);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  line-height: 1.2;
}

.stat-label {
  display: block;
  font-size: 0.75rem;
  color: rgba(255, 255, 255, 0.6);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-top: 0.25rem;
}

/* Right Column - Text */
.about-right {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.about-text {
  margin-bottom: 2rem;
}

.about-text p {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1.1rem;
  line-height: 1.8;
  margin-bottom: 1.25rem;
}

.intro-text {
  font-size: 1.3rem !important;
}

.highlight {
  color: #22d3ee;
  font-weight: 600;
}

.highlight-alt {
  color: #34d399;
  font-weight: 500;
}

.about-text strong {
  color: rgba(255, 255, 255, 0.95);
}

/* Education Badge - Under about text, left aligned */
.education-badge {
  display: flex;
  align-items: center;
  gap: 1.25rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  padding: 1.25rem 2rem;
  width: fit-content;
}

.edu-icon-wrapper {
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.2), rgba(16, 185, 129, 0.2));
  border-radius: 12px;
  color: #22d3ee;
}

.edu-info {
  display: flex;
  flex-direction: column;
}

.edu-school {
  font-weight: 600;
  color: rgba(255, 255, 255, 0.9);
  font-size: 1.1rem;
}

.edu-degree {
  color: rgba(34, 211, 238, 0.8);
  font-size: 0.9rem;
}

/* Academic Section */
.academic-section {
  margin-top: 4rem;
}

.academic-title {
  text-align: center;
  font-size: 1.75rem;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 0.5rem;
  font-weight: 600;
}

.academic-subtitle {
  text-align: center;
  color: rgba(255, 255, 255, 0.5);
  font-size: 1rem;
  margin-bottom: 2.5rem;
}

.courses-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}

.course-card {
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 16px;
  padding: 1.5rem;
  text-align: center;
  transition: all 0.3s ease;
  animation: fadeInUp 0.6s ease-out forwards;
  opacity: 0;
}

.course-card:hover {
  background: rgba(255, 255, 255, 0.05);
  border-color: rgba(34, 211, 238, 0.3);
  transform: translateY(-8px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

.course-icon {
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1rem;
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.15), rgba(16, 185, 129, 0.15));
  border-radius: 12px;
  color: #22d3ee;
  transition: all 0.3s ease;
}

.course-card:hover .course-icon {
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.3), rgba(16, 185, 129, 0.3));
  transform: scale(1.1);
  color: #34d399;
}

.course-title {
  font-size: 1rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 0.5rem;
}

.course-desc {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.5);
  line-height: 1.5;
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

/* Section Footer */
.section-footer {
  text-align: center;
  margin-top: 3rem;
}

/* Responsive */
@media (max-width: 1024px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }

  .about-left {
    align-items: center;
  }

  .courses-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .about-section {
    padding: 4rem 1.5rem;
  }

  .section-title {
    font-size: clamp(2rem, 6vw, 2.5rem);
  }

  .about-text p {
    font-size: 0.95rem;
    line-height: 1.7;
  }

  .courses-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
  }

  .course-card {
    padding: 1.25rem;
  }

  .course-icon {
    width: 48px;
    height: 48px;
  }

  .course-title {
    font-size: 0.9rem;
  }

  .course-desc {
    font-size: 0.8rem;
  }
}

@media (max-width: 640px) {
  .about-section {
    padding: 3rem 1rem;
  }

  .courses-grid {
    grid-template-columns: 1fr;
    gap: 0.75rem;
  }

  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 0.75rem;
  }

  .stat-item {
    padding: 1rem;
  }

  .stat-number {
    font-size: 1.5rem;
  }

  .photo-frame {
    width: 220px;
    height: 260px;
  }

  .education-badge {
    flex-direction: column;
    text-align: center;
    padding: 1rem 1.25rem;
  }

  .edu-icon-wrapper {
    margin: 0 auto;
  }

  .academic-title {
    font-size: 1.4rem;
  }

  .academic-subtitle {
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .about-section {
    padding: 2.5rem 0.75rem;
  }

  .section-header {
    margin-bottom: 2rem;
  }

  .section-tag {
    font-size: 0.85rem;
  }

  .intro-text {
    font-size: 1rem;
  }

  .about-text p {
    font-size: 0.9rem;
  }

  .photo-frame {
    width: 180px;
    height: 220px;
  }

  .stats-grid {
    gap: 0.5rem;
  }

  .stat-item {
    padding: 0.75rem;
    border-radius: 10px;
  }

  .stat-number {
    font-size: 1.3rem;
  }

  .stat-label {
    font-size: 0.7rem;
  }

  .course-card {
    padding: 1rem;
  }

  .course-icon {
    width: 40px;
    height: 40px;
    margin-bottom: 0.75rem;
  }

  .course-icon svg {
    width: 24px;
    height: 24px;
  }
}
</style>
