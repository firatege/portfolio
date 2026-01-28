<script setup>
import { ref, onMounted } from 'vue'
import { Icon } from '@iconify/vue'
import {
  Calendar,
  MapPin,
  Building2
} from 'lucide-vue-next'

const isVisible = ref(false)

const experiences = [
  {
    id: 1,
    role: 'Software Developer & Data Analyst',
    company: 'İntten',
    type: 'Full-time',
    period: 'Present',
    location: 'İzmir, Turkey',
    description: 'Working on data analysis pipelines and software development. Building scalable solutions for data-driven decision making.',
    skills: ['Python', 'SQL', 'Data Analysis', 'Backend Development'],
    icon: 'carbon:analytics',
    current: true
  },
  {
    id: 2,
    role: 'Backend Developer',
    company: 'Moonteeq',
    type: 'Part-time',
    period: 'Present',
    location: 'Remote',
    description: 'Developing high-performance backend systems with modern technologies. Building scalable microservices and real-time data pipelines.',
    skills: ['Rust', 'Redis', 'Docker', 'PostgreSQL'],
    icon: 'carbon:cloud-services',
    current: true
  },
  {
    id: 3,
    role: 'Data Scientist Intern',
    company: 'İntten',
    type: 'Internship',
    period: '2 Months',
    location: 'İzmir, Turkey',
    description: 'Applied machine learning models to real-world business problems. Conducted data preprocessing and feature engineering.',
    skills: ['Python', 'Machine Learning', 'Pandas', 'Scikit-learn'],
    icon: 'carbon:machine-learning',
    current: false
  },
  {
    id: 4,
    role: 'Part-time Data Scientist',
    company: 'Dokuz Eylül University',
    type: 'Part-time',
    period: '1 Year',
    location: 'İzmir, Turkey',
    description: 'Developed simulations and visualizations for university ranking analysis. Built analytical dashboards and predictive models for academic data.',
    skills: ['Python', 'Data Mining', 'Statistical Analysis', 'Visualization'],
    icon: 'carbon:education',
    current: false
  }
]

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true
        }
      })
    },
    { threshold: 0.1 }
  )

  const section = document.querySelector('.experience-section')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="experience" class="experience-section">
    <!-- Background - Connected Nodes Network -->
    <div class="experience-bg">
      <div class="bg-gradient"></div>

      <!-- Network Grid -->
      <svg class="network-svg" viewBox="0 0 1000 800" preserveAspectRatio="xMidYMid slice">
        <!-- Connection Lines -->
        <g class="connections">
          <line x1="100" y1="100" x2="300" y2="200" class="connection-line" />
          <line x1="300" y1="200" x2="500" y2="150" class="connection-line delay-1" />
          <line x1="500" y1="150" x2="700" y2="250" class="connection-line delay-2" />
          <line x1="700" y1="250" x2="900" y2="180" class="connection-line delay-3" />
          <line x1="200" y1="400" x2="400" y2="350" class="connection-line delay-2" />
          <line x1="400" y1="350" x2="600" y2="450" class="connection-line delay-1" />
          <line x1="600" y1="450" x2="800" y2="400" class="connection-line delay-3" />
          <line x1="150" y1="600" x2="350" y2="550" class="connection-line delay-1" />
          <line x1="350" y1="550" x2="550" y2="650" class="connection-line delay-2" />
          <line x1="550" y1="650" x2="750" y2="580" class="connection-line delay-3" />
          <line x1="750" y1="580" x2="900" y2="650" class="connection-line" />
          <!-- Vertical connections -->
          <line x1="300" y1="200" x2="400" y2="350" class="connection-line delay-2" />
          <line x1="500" y1="150" x2="600" y2="450" class="connection-line delay-1" />
          <line x1="700" y1="250" x2="750" y2="580" class="connection-line delay-3" />
          <line x1="200" y1="400" x2="350" y2="550" class="connection-line" />
        </g>

        <!-- Data Flow Particles -->
        <g class="particles">
          <circle r="3" class="particle particle-1">
            <animateMotion dur="4s" repeatCount="indefinite" path="M100,100 L300,200 L500,150 L700,250" />
          </circle>
          <circle r="2" class="particle particle-2">
            <animateMotion dur="5s" repeatCount="indefinite" path="M200,400 L400,350 L600,450 L800,400" />
          </circle>
          <circle r="3" class="particle particle-3">
            <animateMotion dur="6s" repeatCount="indefinite" path="M150,600 L350,550 L550,650 L750,580" />
          </circle>
          <circle r="2" class="particle particle-4">
            <animateMotion dur="3s" repeatCount="indefinite" path="M300,200 L400,350 L350,550" />
          </circle>
        </g>

        <!-- Nodes -->
        <g class="nodes">
          <circle cx="100" cy="100" r="6" class="node node-1" />
          <circle cx="300" cy="200" r="8" class="node node-2" />
          <circle cx="500" cy="150" r="6" class="node node-3" />
          <circle cx="700" cy="250" r="8" class="node node-4" />
          <circle cx="900" cy="180" r="6" class="node node-1" />
          <circle cx="200" cy="400" r="6" class="node node-2" />
          <circle cx="400" cy="350" r="8" class="node node-3" />
          <circle cx="600" cy="450" r="6" class="node node-4" />
          <circle cx="800" cy="400" r="8" class="node node-1" />
          <circle cx="150" cy="600" r="6" class="node node-2" />
          <circle cx="350" cy="550" r="8" class="node node-3" />
          <circle cx="550" cy="650" r="6" class="node node-4" />
          <circle cx="750" cy="580" r="8" class="node node-1" />
          <circle cx="900" cy="650" r="6" class="node node-2" />
        </g>
      </svg>

      <!-- Floating Code Symbols -->
      <div class="floating-code">
        <span class="code-symbol sym-1">{}</span>
        <span class="code-symbol sym-2">&lt;/&gt;</span>
        <span class="code-symbol sym-3">01</span>
        <span class="code-symbol sym-4">λ</span>
        <span class="code-symbol sym-5">∑</span>
      </div>
    </div>

    <div class="experience-container" :class="{ 'visible': isVisible }">
      <!-- Section Header -->
      <div class="section-header">
        <span class="section-tag">&lt;experience&gt;</span>
        <h2 class="section-title">Work Experience</h2>
        <div class="title-underline"></div>
      </div>

      <!-- Timeline -->
      <div class="timeline">
        <div class="timeline-line"></div>

        <div
          v-for="(exp, index) in experiences"
          :key="exp.id"
          class="timeline-item"
          :class="{ 'current': exp.current }"
          :style="{ animationDelay: `${index * 0.15}s` }"
        >
          <!-- Timeline Node -->
          <div class="timeline-node">
            <div class="node-icon">
              <Icon :icon="exp.icon" width="24" height="24" />
            </div>
            <div class="node-pulse" v-if="exp.current"></div>
          </div>

          <!-- Experience Card -->
          <div class="exp-card">
            <div class="exp-header">
              <div class="exp-title-group">
                <h3 class="exp-role">{{ exp.role }}</h3>
                <div class="exp-company">
                  <Building2 :size="16" />
                  <span>{{ exp.company }}</span>
                </div>
              </div>
              <div class="exp-meta">
                <span class="exp-type" :class="exp.type.toLowerCase().replace('-', '')">
                  {{ exp.type }}
                </span>
                <span class="exp-period" v-if="exp.current">
                  <span class="current-badge">Current</span>
                </span>
                <span class="exp-period" v-else>
                  <Calendar :size="14" />
                  {{ exp.period }}
                </span>
              </div>
            </div>

            <div class="exp-location">
              <MapPin :size="14" />
              <span>{{ exp.location }}</span>
            </div>

            <p class="exp-description">{{ exp.description }}</p>

            <div class="exp-skills">
              <span
                v-for="skill in exp.skills"
                :key="skill"
                class="skill-tag"
              >
                {{ skill }}
              </span>
            </div>
          </div>
        </div>
      </div>

      <!-- Section Footer -->
      <div class="section-footer">
        <span class="section-tag">&lt;/experience&gt;</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.experience-section {
  min-height: 100vh;
  padding: 6rem 2rem;
  position: relative;
  overflow: hidden;
  background: radial-gradient(ellipse at 50% 50%, #0c1929 0%, #070d15 100%);
}

/* Background */
.experience-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
  overflow: hidden;
}

.bg-gradient {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 800px;
  height: 800px;
  background: radial-gradient(circle, rgba(6, 182, 212, 0.06) 0%, transparent 70%);
  filter: blur(60px);
}

/* Network SVG */
.network-svg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.15;
}

/* Connection Lines */
.connection-line {
  stroke: rgba(34, 211, 238, 0.08);
  stroke-width: 1;
  stroke-dasharray: 8 8;
  animation: dashFlow 40s linear infinite;
}

.connection-line.delay-1 { animation-delay: -10s; }
.connection-line.delay-2 { animation-delay: -20s; }
.connection-line.delay-3 { animation-delay: -30s; }

@keyframes dashFlow {
  0% { stroke-dashoffset: 0; }
  100% { stroke-dashoffset: -200; }
}

/* Nodes */
.node {
  fill: rgba(34, 211, 238, 0.15);
  animation: nodePulse 6s ease-in-out infinite;
}

.node-1 { animation-delay: 0s; }
.node-2 { animation-delay: 1s; fill: rgba(16, 185, 129, 0.15); }
.node-3 { animation-delay: 2s; }
.node-4 { animation-delay: 3s; fill: rgba(139, 92, 246, 0.15); }

@keyframes nodePulse {
  0%, 100% { opacity: 0.15; transform: scale(1); }
  50% { opacity: 0.25; transform: scale(1.1); }
}

/* Particles */
.particle {
  fill: rgba(34, 211, 238, 0.4);
  filter: drop-shadow(0 0 2px rgba(34, 211, 238, 0.4));
}

.particle-1 { fill: rgba(34, 211, 238, 0.4); }
.particle-2 { fill: rgba(16, 185, 129, 0.4); }
.particle-3 { fill: rgba(139, 92, 246, 0.4); }
.particle-4 { fill: rgba(34, 211, 238, 0.4); }

/* Floating Code Symbols */
.floating-code {
  position: absolute;
  width: 100%;
  height: 100%;
}

.code-symbol {
  position: absolute;
  font-family: 'Fira Code', monospace;
  font-size: 1.2rem;
  color: rgba(34, 211, 238, 0.04);
  animation: floatSymbol 35s ease-in-out infinite;
}

.sym-1 { top: 15%; left: 5%; animation-delay: 0s; }
.sym-2 { top: 25%; right: 8%; animation-delay: 7s; color: rgba(16, 185, 129, 0.04); }
.sym-3 { top: 60%; left: 8%; animation-delay: 14s; }
.sym-4 { bottom: 20%; right: 12%; animation-delay: 21s; color: rgba(139, 92, 246, 0.04); }
.sym-5 { bottom: 35%; left: 15%; animation-delay: 28s; color: rgba(16, 185, 129, 0.04); }

@keyframes floatSymbol {
  0%, 100% {
    transform: translate(0, 0) rotate(0deg);
    opacity: 0.04;
  }
  25% {
    transform: translate(10px, -15px) rotate(3deg);
    opacity: 0.06;
  }
  50% {
    transform: translate(0, -25px) rotate(0deg);
    opacity: 0.04;
  }
  75% {
    transform: translate(-10px, -10px) rotate(-3deg);
    opacity: 0.06;
  }
}

/* Container */
.experience-container {
  max-width: 900px;
  margin: 0 auto;
  position: relative;
  z-index: 2;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease-out;
}

.experience-container.visible {
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

/* Timeline */
.timeline {
  position: relative;
  padding-left: 60px;
}

.timeline-line {
  position: absolute;
  left: 24px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: linear-gradient(180deg,
    rgba(34, 211, 238, 0.5) 0%,
    rgba(16, 185, 129, 0.3) 50%,
    rgba(139, 92, 246, 0.2) 100%
  );
}

.timeline-item {
  position: relative;
  margin-bottom: 2.5rem;
  opacity: 0;
  transform: translateX(-30px);
  animation: slideIn 0.6s ease-out forwards;
}

@keyframes slideIn {
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Timeline Node */
.timeline-node {
  position: absolute;
  left: -60px;
  top: 20px;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.node-icon {
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(6, 182, 212, 0.15);
  border: 2px solid rgba(34, 211, 238, 0.4);
  border-radius: 50%;
  color: #22d3ee;
  z-index: 2;
  transition: all 0.3s ease;
}

.timeline-item:hover .node-icon {
  background: rgba(6, 182, 212, 0.25);
  border-color: #22d3ee;
  transform: scale(1.1);
}

.timeline-item.current .node-icon {
  background: rgba(16, 185, 129, 0.2);
  border-color: #10b981;
  color: #10b981;
}

.node-pulse {
  position: absolute;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 2px solid #10b981;
  animation: pulse 2s ease-out infinite;
}

@keyframes pulse {
  0% { transform: scale(1); opacity: 0.8; }
  100% { transform: scale(1.8); opacity: 0; }
}

/* Experience Card */
.exp-card {
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  padding: 1.5rem;
  transition: all 0.3s ease;
}

.exp-card:hover {
  background: rgba(255, 255, 255, 0.04);
  border-color: rgba(34, 211, 238, 0.2);
  transform: translateX(10px);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
}

.timeline-item.current .exp-card {
  border-color: rgba(16, 185, 129, 0.3);
}

.exp-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 0.75rem;
  gap: 1rem;
}

.exp-title-group {
  flex: 1;
}

.exp-role {
  font-size: 1.25rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 0.35rem;
}

.exp-company {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #22d3ee;
  font-size: 0.95rem;
}

.exp-meta {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 0.35rem;
}

.exp-type {
  font-size: 0.75rem;
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.exp-type.fulltime {
  background: rgba(16, 185, 129, 0.15);
  color: #10b981;
}

.exp-type.parttime {
  background: rgba(34, 211, 238, 0.15);
  color: #22d3ee;
}

.exp-type.internship {
  background: rgba(139, 92, 246, 0.15);
  color: #a78bfa;
}

.exp-period {
  display: flex;
  align-items: center;
  gap: 0.35rem;
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.5);
}

.current-badge {
  background: linear-gradient(135deg, #10b981, #06b6d4);
  color: white;
  padding: 0.2rem 0.6rem;
  border-radius: 12px;
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.exp-location {
  display: flex;
  align-items: center;
  gap: 0.35rem;
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.4);
  margin-bottom: 1rem;
}

.exp-description {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.6;
  margin-bottom: 1rem;
}

.exp-skills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.skill-tag {
  font-size: 0.75rem;
  padding: 0.3rem 0.75rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  color: rgba(255, 255, 255, 0.7);
  transition: all 0.2s ease;
}

.skill-tag:hover {
  background: rgba(34, 211, 238, 0.1);
  border-color: rgba(34, 211, 238, 0.3);
  color: #22d3ee;
}

/* Section Footer */
.section-footer {
  text-align: center;
  margin-top: 3rem;
}

/* Responsive */
@media (max-width: 768px) {
  .experience-section {
    padding: 4rem 1.5rem;
  }

  .section-title {
    font-size: clamp(2rem, 6vw, 2.5rem);
  }

  .timeline {
    padding-left: 50px;
  }

  .timeline-line {
    left: 18px;
  }

  .timeline-node {
    left: -50px;
    width: 40px;
    height: 40px;
  }

  .node-icon {
    width: 40px;
    height: 40px;
  }

  .node-pulse {
    width: 40px;
    height: 40px;
  }

  .exp-header {
    flex-direction: column;
    gap: 0.75rem;
  }

  .exp-meta {
    flex-direction: row;
    align-items: center;
  }

  .exp-role {
    font-size: 1.1rem;
  }

  .exp-card {
    padding: 1.25rem;
  }

  .exp-description {
    font-size: 0.85rem;
  }

  .network-svg {
    opacity: 0.08;
  }

  .floating-code {
    display: none;
  }
}

@media (max-width: 640px) {
  .experience-section {
    padding: 3rem 1rem;
  }

  .timeline {
    padding-left: 45px;
  }

  .timeline-line {
    left: 16px;
  }

  .timeline-node {
    left: -45px;
    width: 36px;
    height: 36px;
  }

  .node-icon {
    width: 36px;
    height: 36px;
  }

  .node-icon svg {
    width: 18px;
    height: 18px;
  }

  .node-pulse {
    width: 36px;
    height: 36px;
  }

  .exp-card {
    padding: 1rem;
    border-radius: 12px;
  }

  .exp-role {
    font-size: 1rem;
  }

  .exp-company {
    font-size: 0.85rem;
  }

  .exp-type {
    font-size: 0.65rem;
    padding: 0.2rem 0.5rem;
  }

  .exp-description {
    font-size: 0.8rem;
    line-height: 1.5;
  }

  .skill-tag {
    font-size: 0.7rem;
    padding: 0.25rem 0.6rem;
  }
}

@media (max-width: 480px) {
  .experience-section {
    padding: 2.5rem 0.75rem;
  }

  .section-header {
    margin-bottom: 2rem;
  }

  .section-tag {
    font-size: 0.85rem;
  }

  .timeline {
    padding-left: 40px;
  }

  .timeline-line {
    left: 14px;
  }

  .timeline-node {
    left: -40px;
    width: 32px;
    height: 32px;
  }

  .node-icon {
    width: 32px;
    height: 32px;
  }

  .node-icon svg {
    width: 16px;
    height: 16px;
  }

  .node-pulse {
    width: 32px;
    height: 32px;
  }

  .exp-card {
    padding: 0.875rem;
  }

  .exp-role {
    font-size: 0.95rem;
    line-height: 1.3;
  }

  .exp-company span {
    font-size: 0.8rem;
  }

  .exp-meta {
    gap: 0.5rem;
    flex-wrap: wrap;
  }

  .exp-location {
    font-size: 0.75rem;
    margin-bottom: 0.75rem;
  }

  .exp-description {
    font-size: 0.75rem;
    margin-bottom: 0.75rem;
  }

  .exp-skills {
    gap: 0.35rem;
  }

  .skill-tag {
    font-size: 0.65rem;
    padding: 0.2rem 0.5rem;
  }
}
</style>
