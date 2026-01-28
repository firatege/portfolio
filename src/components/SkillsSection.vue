<script setup>
import { ref, computed, onMounted } from 'vue'
import { Icon } from '@iconify/vue'
import {
  Code2,
  Brain,
  Server,
  Database,
  Cloud,
  BarChart3,
  Cpu,
  Network,
  Workflow,
  Globe,
  LineChart
} from 'lucide-vue-next'

const isVisible = ref(false)
const activeCategory = ref(0)

// Skill categories with orbit items (using iconify icon names for orbit)
const categories = [
  {
    id: 'languages',
    title: 'Languages',
    icon: 'code',
    skills: [
      { name: 'Python', desc: 'Data analysis, ML, Backend', icon: 'logos:python' },
      { name: 'JavaScript', desc: 'Web interfaces, Client-side', icon: 'logos:javascript' },
      { name: 'TypeScript', desc: 'Type-safe JavaScript development', icon: 'logos:typescript-icon' },
      { name: 'Rust', desc: 'Performance & safe systems', icon: 'logos:rust' }
    ],
    orbit: [
      { icon: 'logos:python', label: 'Py' },
      { icon: 'logos:javascript', label: 'JS' },
      { icon: 'logos:typescript-icon', label: 'TS' },
      { icon: 'logos:rust', label: 'Rs' }
    ]
  },
  {
    id: 'ai-data',
    title: 'AI & Data',
    icon: 'brain',
    skills: [
      { name: 'Machine Learning', desc: 'Supervised & unsupervised learning', icon: 'lucide:cpu' },
      { name: 'Deep Learning', desc: 'Neural networks, TensorFlow/Keras', icon: 'logos:tensorflow' },
      { name: 'NLP', desc: 'TF-IDF, similarity search, intent', icon: 'lucide:brain' },
      { name: 'RAG Systems', desc: 'Retrieval-augmented generation', icon: 'lucide:workflow' }
    ],
    orbit: [
      { icon: 'carbon:machine-learning', label: 'ML' },
      { icon: 'logos:tensorflow', label: 'TF' },
      { icon: 'carbon:text-link-analysis', label: 'NLP' },
      { icon: 'carbon:data-enrichment', label: 'RAG' }
    ]
  },
  {
    id: 'backend',
    title: 'Backend & API',
    icon: 'server',
    skills: [
      { name: 'FastAPI', desc: 'Python async web framework', icon: 'logos:fastapi-icon' },
      { name: 'NestJS', desc: 'Node.js enterprise framework', icon: 'logos:nestjs' },
      { name: 'Express', desc: 'Minimalist Node.js framework', icon: 'simple-icons:express' },
      { name: 'Actix Web', desc: 'Rust web framework', icon: 'logos:rust' },
      { name: 'REST API', desc: 'RESTful service design', icon: 'lucide:globe' },
      { name: 'WebSocket', desc: 'Real-time communication', icon: 'lucide:network' }
    ],
    orbit: [
      { icon: 'logos:fastapi-icon', label: 'Fast' },
      { icon: 'logos:nestjs', label: 'Nest' },
      { icon: 'simple-icons:express', label: 'Exp' },
      { icon: 'carbon:api', label: 'API' },
      { icon: 'carbon:cloud-services', label: 'WS' },
      { icon: 'logos:rust', label: 'Actix' }
    ]
  },
  {
    id: 'databases',
    title: 'Databases',
    icon: 'database',
    skills: [
      { name: 'PostgreSQL', desc: 'Relational database', icon: 'logos:postgresql' },
      { name: 'MongoDB', desc: 'NoSQL document store', icon: 'logos:mongodb-icon' },
      { name: 'Redis', desc: 'Cache & ephemeral data', icon: 'logos:redis' },
      { name: 'pgvector', desc: 'Vector embeddings', icon: 'lucide:cpu' }
    ],
    orbit: [
      { icon: 'logos:postgresql', label: 'PG' },
      { icon: 'logos:mongodb-icon', label: 'Mongo' },
      { icon: 'logos:redis', label: 'Redis' },
      { icon: 'carbon:data-vis-4', label: 'Vec' }
    ]
  },
  {
    id: 'visualization',
    title: 'Visualization',
    icon: 'chart',
    skills: [
      { name: 'Power BI', desc: 'Business intelligence dashboards', icon: 'logos:microsoft-power-bi' },
      { name: 'Excel', desc: 'Advanced data analysis & reporting', icon: 'vscode-icons:file-type-excel' },
      { name: 'Matplotlib', desc: 'Python plotting library', icon: 'lucide:line-chart' },
      { name: 'Chart.js', desc: 'Interactive web charts', icon: 'simple-icons:chartdotjs' }
    ],
    orbit: [
      { icon: 'logos:microsoft-power-bi', label: 'PBI' },
      { icon: 'vscode-icons:file-type-excel', label: 'Excel' },
      { icon: 'carbon:chart-line', label: 'MPL' },
      { icon: 'simple-icons:chartdotjs', label: 'Chart' }
    ]
  },
  {
    id: 'devops',
    title: 'DevOps & Tools',
    icon: 'cloud',
    skills: [
      { name: 'Kubernetes', desc: 'Container orchestration', icon: 'logos:kubernetes' },
      { name: 'Docker', desc: 'Containerization', icon: 'logos:docker-icon' },
      { name: 'Git', desc: 'Version control', icon: 'logos:git-icon' },
      { name: 'Linux', desc: 'System administration', icon: 'logos:linux-tux' }
    ],
    orbit: [
      { icon: 'logos:kubernetes', label: 'K8s' },
      { icon: 'logos:docker-icon', label: 'Docker' },
      { icon: 'logos:git-icon', label: 'Git' },
      { icon: 'logos:linux-tux', label: 'Linux' }
    ]
  }
]

// Current category's orbit items
const currentOrbit = computed(() => categories[activeCategory.value].orbit)

// Current skills (for fixing transition bug)
const currentSkills = computed(() => categories[activeCategory.value].skills)

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

  const section = document.querySelector('.skills-section')
  if (section) observer.observe(section)
})

function setCategory(index) {
  activeCategory.value = index
}
</script>

<template>
  <section id="skills" class="skills-section">
    <!-- Background elements -->
    <div class="skills-bg">
      <div class="grid-lines"></div>
      <div class="floating-shapes">
        <div class="shape shape-1"></div>
        <div class="shape shape-2"></div>
        <div class="shape shape-3"></div>
      </div>
    </div>

    <div class="skills-container" :class="{ 'visible': isVisible }">
      <!-- Tech Icons Orbit - Large background element -->
      <div class="tech-orbit">
        <div class="orbit-ring ring-outer">
          <div
            v-for="(item, index) in currentOrbit"
            :key="`orbit-outer-${activeCategory}-${index}`"
            class="orbit-item"
            :style="{ '--angle': `${(360 / currentOrbit.length) * index}deg`, '--distance': '380px' }"
          >
            <span class="orbit-icon">
              <Icon :icon="item.icon" width="28" height="28" />
            </span>
          </div>
        </div>
        <div class="orbit-ring ring-middle">
          <div
            v-for="(item, index) in currentOrbit"
            :key="`orbit-middle-${activeCategory}-${index}`"
            class="orbit-item orbit-item-sm"
            :style="{ '--angle': `${(360 / currentOrbit.length) * index + 45}deg`, '--distance': '255px' }"
          >
            <span class="orbit-icon-sm">
              <Icon :icon="item.icon" width="18" height="18" />
            </span>
          </div>
        </div>
        <div class="orbit-ring ring-inner">
          <div
            v-for="(item, index) in currentOrbit"
            :key="`orbit-inner-${activeCategory}-${index}`"
            class="orbit-item orbit-item-xs"
            :style="{ '--angle': `${(360 / currentOrbit.length) * index + 90}deg`, '--distance': '130px' }"
          >
            <span class="orbit-dot"></span>
          </div>
        </div>
        <div class="orbit-center">
          <span>FEB</span>
        </div>
      </div>

      <!-- Section Header -->
      <div class="section-header">
        <span class="section-tag">&lt;skills&gt;</span>
        <h2 class="section-title">Tech Stack</h2>
        <div class="title-underline"></div>
      </div>

      <!-- Skills Content -->
      <div class="skills-content">
        <!-- Category Tabs -->
        <div class="category-tabs">
          <button
            v-for="(category, index) in categories"
            :key="category.id"
            class="category-tab"
            :class="{ 'active': activeCategory === index }"
            @click="setCategory(index)"
          >
            <div class="tab-icon">
              <Code2 v-if="category.icon === 'code'" :size="20" />
              <Brain v-if="category.icon === 'brain'" :size="20" />
              <Server v-if="category.icon === 'server'" :size="20" />
              <Database v-if="category.icon === 'database'" :size="20" />
              <Cloud v-if="category.icon === 'cloud'" :size="20" />
              <BarChart3 v-if="category.icon === 'chart'" :size="20" />
            </div>
            <span class="tab-title">{{ category.title }}</span>
            <div class="tab-indicator"></div>
          </button>
        </div>

        <!-- Skills Display -->
        <div class="skills-display">
          <div class="skills-grid">
            <div
              v-for="(skill, index) in currentSkills"
              :key="`${activeCategory}-${skill.name}`"
              class="skill-card"
              :style="{ animationDelay: `${index * 0.1}s` }"
            >
              <div class="skill-icon">
                <!-- Iconify icons (logos, brand icons) -->
                <Icon v-if="skill.icon.startsWith('logos:') || skill.icon.startsWith('simple-icons:') || skill.icon.startsWith('vscode-icons:')" :icon="skill.icon" width="28" height="28" />
                <!-- Lucide icons -->
                <Cpu v-else-if="skill.icon === 'lucide:cpu'" :size="24" />
                <Brain v-else-if="skill.icon === 'lucide:brain'" :size="24" />
                <Workflow v-else-if="skill.icon === 'lucide:workflow'" :size="24" />
                <Globe v-else-if="skill.icon === 'lucide:globe'" :size="24" />
                <Network v-else-if="skill.icon === 'lucide:network'" :size="24" />
                <LineChart v-else-if="skill.icon === 'lucide:line-chart'" :size="24" />
              </div>
              <div class="skill-info">
                <h4 class="skill-name">{{ skill.name }}</h4>
                <p class="skill-desc">{{ skill.desc }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Section Footer -->
      <div class="section-footer">
        <span class="section-tag">&lt;/skills&gt;</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills-section {
  min-height: 100vh;
  padding: 6rem 2rem;
  position: relative;
  overflow: hidden;
  background: radial-gradient(ellipse at 50% 50%, #0c1929 0%, #070d15 100%);
}

/* Background */
.skills-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

.grid-lines {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image:
    linear-gradient(rgba(34, 211, 238, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(34, 211, 238, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: gridMove 20s linear infinite;
}

@keyframes gridMove {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}

.floating-shapes {
  position: absolute;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.15;
}

.shape-1 {
  width: 400px;
  height: 400px;
  background: #06b6d4;
  top: 10%;
  right: -100px;
  animation: floatShape 15s ease-in-out infinite;
}

.shape-2 {
  width: 300px;
  height: 300px;
  background: #10b981;
  bottom: 20%;
  left: -50px;
  animation: floatShape 18s ease-in-out infinite reverse;
}

.shape-3 {
  width: 250px;
  height: 250px;
  background: #8b5cf6;
  top: 50%;
  left: 50%;
  animation: floatShape 12s ease-in-out infinite;
}

@keyframes floatShape {
  0%, 100% { transform: translate(0, 0) scale(1); }
  50% { transform: translate(30px, -30px) scale(1.1); }
}

/* Container */
.skills-container {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 2;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease-out;
}

.skills-container.visible {
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

/* Skills Content */
.skills-content {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 3rem;
  margin-bottom: 4rem;
}

/* Category Tabs */
.category-tabs {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.category-tab {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem 1.25rem;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.category-tab:hover {
  background: rgba(255, 255, 255, 0.05);
  border-color: rgba(34, 211, 238, 0.2);
}

.category-tab.active {
  background: rgba(34, 211, 238, 0.1);
  border-color: rgba(34, 211, 238, 0.4);
}

.tab-icon {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 10px;
  color: rgba(255, 255, 255, 0.6);
  transition: all 0.3s ease;
}

.category-tab.active .tab-icon {
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.3), rgba(16, 185, 129, 0.3));
  color: #22d3ee;
}

.tab-title {
  font-size: 0.95rem;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.7);
  transition: all 0.3s ease;
}

.category-tab.active .tab-title {
  color: #22d3ee;
}

.tab-indicator {
  position: absolute;
  left: 0;
  top: 0;
  width: 3px;
  height: 100%;
  background: linear-gradient(180deg, #06b6d4, #10b981);
  transform: scaleY(0);
  transition: transform 0.3s ease;
}

.category-tab.active .tab-indicator {
  transform: scaleY(1);
}

/* Skills Display */
.skills-display {
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 20px;
  padding: 2rem;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.25rem;
}

.skill-card {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 14px;
  padding: 1.25rem;
  transition: all 0.3s ease;
  animation: skillCardIn 0.5s ease-out forwards;
  opacity: 0;
  transform: translateY(20px);
}

.skill-card:hover {
  background: rgba(34, 211, 238, 0.08);
  border-color: rgba(34, 211, 238, 0.3);
  transform: translateY(-5px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
}

.skill-card:hover .skill-icon {
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.3), rgba(16, 185, 129, 0.3));
  color: #22d3ee;
  transform: scale(1.1);
}

@keyframes skillCardIn {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.skill-icon {
  width: 48px;
  height: 48px;
  min-width: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 12px;
  color: rgba(255, 255, 255, 0.6);
  transition: all 0.3s ease;
}

.skill-info {
  flex: 1;
}

.skill-name {
  font-weight: 600;
  color: #22d3ee;
  font-size: 1rem;
  margin-bottom: 0.35rem;
}

.skill-desc {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.5);
  line-height: 1.4;
  margin: 0;
}

/* Tech Orbit - Large background element with nested rings */
.tech-orbit {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 900px;
  height: 900px;
  opacity: 0.18;
  z-index: 1;
  pointer-events: none;
}

/* Orbit Rings */
.orbit-ring {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border: 1px dashed rgba(34, 211, 238, 0.25);
  border-radius: 50%;
}

.ring-outer {
  width: 800px;
  height: 800px;
  animation: orbitRotate 50s linear infinite;
  box-shadow:
    0 0 30px rgba(34, 211, 238, 0.05),
    inset 0 0 30px rgba(34, 211, 238, 0.03);
}

.ring-middle {
  width: 550px;
  height: 550px;
  border-color: rgba(16, 185, 129, 0.25);
  animation: orbitRotate 38s linear infinite reverse;
  box-shadow:
    0 0 25px rgba(16, 185, 129, 0.05),
    inset 0 0 25px rgba(16, 185, 129, 0.03);
}

.ring-inner {
  width: 300px;
  height: 300px;
  border-color: rgba(139, 92, 246, 0.25);
  animation: orbitRotate 25s linear infinite;
  box-shadow:
    0 0 20px rgba(139, 92, 246, 0.05),
    inset 0 0 20px rgba(139, 92, 246, 0.03);
}

@keyframes orbitRotate {
  from { transform: translate(-50%, -50%) rotate(0deg); }
  to { transform: translate(-50%, -50%) rotate(360deg); }
}

/* Orbit Items */
.orbit-item {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 55px;
  height: 55px;
  margin: -27.5px;
  transform: rotate(var(--angle)) translateX(var(--distance)) rotate(calc(-1 * var(--angle)));
  transition: all 0.5s ease;
}

.orbit-item-sm {
  width: 40px;
  height: 40px;
  margin: -20px;
}

.orbit-item-xs {
  width: 12px;
  height: 12px;
  margin: -6px;
}

.orbit-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background: rgba(6, 182, 212, 0.08);
  border: 1px solid rgba(34, 211, 238, 0.2);
  border-radius: 12px;
  color: rgba(34, 211, 238, 0.7);
  backdrop-filter: blur(3px);
  box-shadow: 0 0 15px rgba(34, 211, 238, 0.1);
  animation: orbitItemFloat 6s ease-in-out infinite;
}

.orbit-icon-sm {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background: rgba(16, 185, 129, 0.08);
  border: 1px solid rgba(52, 211, 153, 0.2);
  border-radius: 10px;
  color: rgba(52, 211, 153, 0.7);
  box-shadow: 0 0 12px rgba(52, 211, 153, 0.1);
  animation: orbitItemFloat 8s ease-in-out infinite reverse;
}

.orbit-dot {
  display: block;
  width: 100%;
  height: 100%;
  background: rgba(139, 92, 246, 0.4);
  border: 1px solid rgba(139, 92, 246, 0.5);
  border-radius: 50%;
  box-shadow: 0 0 10px rgba(139, 92, 246, 0.3);
  animation: dotFloat 4s ease-in-out infinite;
}

@keyframes orbitItemFloat {
  0%, 100% {
    opacity: 0.6;
    transform: scale(1);
  }
  50% {
    opacity: 0.9;
    transform: scale(1.05);
  }
}

@keyframes dotFloat {
  0%, 100% {
    opacity: 0.5;
    transform: scale(1);
  }
  50% {
    opacity: 0.8;
    transform: scale(1.15);
  }
}

.orbit-center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 90px;
  height: 90px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.1), rgba(16, 185, 129, 0.1));
  border: 1px solid rgba(34, 211, 238, 0.3);
  border-radius: 50%;
  color: rgba(34, 211, 238, 0.8);
  font-weight: 800;
  font-size: 1.3rem;
  font-family: 'Fira Code', monospace;
  box-shadow:
    0 0 30px rgba(34, 211, 238, 0.15),
    0 0 60px rgba(16, 185, 129, 0.08);
  animation: centerFloat 5s ease-in-out infinite;
}

@keyframes centerFloat {
  0%, 100% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 0.7;
  }
  50% {
    transform: translate(-50%, -50%) scale(1.05);
    opacity: 0.9;
  }
}

/* Responsive - Show orbit on larger screens */
@media (max-width: 1100px) {
  .tech-orbit {
    opacity: 0.12;
    width: 700px;
    height: 700px;
  }

  .ring-outer {
    width: 600px;
    height: 600px;
  }

  .ring-middle {
    width: 420px;
    height: 420px;
  }

  .ring-inner {
    width: 240px;
    height: 240px;
  }
}

/* Section Footer */
.section-footer {
  text-align: center;
  margin-top: 3rem;
}

/* Responsive */
@media (max-width: 900px) {
  .skills-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .category-tabs {
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }

  .category-tab {
    flex: 0 0 auto;
    padding: 0.75rem 1rem;
  }

  .tab-title {
    display: none;
  }

  .tab-indicator {
    width: 100%;
    height: 3px;
    top: auto;
    bottom: 0;
    transform: scaleX(0);
  }

  .category-tab.active .tab-indicator {
    transform: scaleX(1);
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .skills-section {
    padding: 4rem 1.5rem;
  }

  .tech-orbit {
    display: none;
  }

  .section-title {
    font-size: clamp(2rem, 6vw, 2.5rem);
  }

  .category-tabs {
    gap: 0.5rem;
    padding: 0.5rem;
    background: rgba(255, 255, 255, 0.02);
    border-radius: 12px;
  }

  .category-tab {
    padding: 0.6rem 0.8rem;
    border-radius: 8px;
  }

  .tab-icon {
    width: 36px;
    height: 36px;
  }

  .skills-display {
    padding: 1.5rem;
  }

  .skill-card {
    padding: 1rem;
  }

  .skill-icon {
    width: 44px;
    height: 44px;
  }

  .skill-name {
    font-size: 0.95rem;
  }

  .skill-desc {
    font-size: 0.8rem;
  }
}

@media (max-width: 640px) {
  .skills-section {
    padding: 3rem 1rem;
  }

  .skills-display {
    padding: 1rem;
    border-radius: 12px;
  }

  .skills-grid {
    gap: 0.75rem;
  }

  .skill-card {
    padding: 0.875rem;
    border-radius: 10px;
    gap: 0.75rem;
  }

  .skill-icon {
    width: 40px;
    height: 40px;
    border-radius: 8px;
  }
}

@media (max-width: 480px) {
  .skills-section {
    padding: 2.5rem 0.75rem;
  }

  .section-header {
    margin-bottom: 1.5rem;
  }

  .section-tag {
    font-size: 0.85rem;
  }

  .category-tabs {
    gap: 0.4rem;
    padding: 0.4rem;
  }

  .category-tab {
    padding: 0.5rem 0.6rem;
  }

  .tab-icon {
    width: 32px;
    height: 32px;
  }

  .tab-icon svg {
    width: 16px;
    height: 16px;
  }

  .skill-card {
    padding: 0.75rem;
  }

  .skill-icon {
    width: 36px;
    height: 36px;
  }

  .skill-icon svg {
    width: 18px;
    height: 18px;
  }

  .skill-name {
    font-size: 0.9rem;
  }

  .skill-desc {
    font-size: 0.75rem;
    line-height: 1.4;
  }
}
</style>
