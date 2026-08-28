<script setup>
import { ref, onMounted } from 'vue'
import { Icon } from '@iconify/vue'
import { ExternalLink, Github, Folder } from 'lucide-vue-next'

const isVisible = ref(false)
const activeFilter = ref('all')

const filters = [
  { id: 'all', label: 'All Projects' },
  { id: 'backend', label: 'Backend' },
  { id: 'ai-data', label: 'AI & Data' },
  { id: 'fullstack', label: 'Full Stack' }
]

const projects = [
  // Backend Projects
  {
    id: 2,
    title: 'BookingAPI-NestJS',
    subtitle: 'RESTful API with NestJS',
    description: 'Learning project exploring NestJS framework with basic API design patterns, authentication, and database integration.',
    category: 'backend',
    tech: [
      { name: 'NestJS', icon: 'logos:nestjs' },
      { name: 'TypeScript', icon: 'logos:typescript-icon' },
      { name: 'PostgreSQL', icon: 'logos:postgresql' }
    ],
    github: 'https://github.com/firatege/BookingAPI-NestJS',
    color: 'green'
  },
  {
    id: 3,
    title: 'Atomic BankNest',
    subtitle: 'Banking API with NestJS',
    description: 'Atomic banking operations API built with NestJS. Implements transaction safety, account management, and financial operations with robust error handling.',
    category: 'backend',
    tech: [
      { name: 'NestJS', icon: 'logos:nestjs' },
      { name: 'TypeScript', icon: 'logos:typescript-icon' },
      { name: 'PostgreSQL', icon: 'logos:postgresql' },
      { name: 'Transactions', icon: 'carbon:currency' }
    ],
    github: 'https://github.com/firatege/atomic-banknest-NESTJS',
    color: 'purple'
  },
  {
    id: 4,
    title: 'Python Blog API',
    subtitle: 'Modern Blog Backend with FastAPI',
    description: 'RESTful API with JWT authentication, role-based authorization, and PostgreSQL integration. Clean architecture with modern Python practices.',
    category: 'backend',
    tech: [
      { name: 'FastAPI', icon: 'logos:fastapi-icon' },
      { name: 'Python', icon: 'logos:python' },
      { name: 'PostgreSQL', icon: 'logos:postgresql' },
      { name: 'JWT', icon: 'carbon:security' }
    ],
    github: 'https://github.com/firatege/python-Blog',
    color: 'cyan'
  },
  // AI & Data Projects
  {
    id: 5,
    title: 'RAG for GTNH',
    subtitle: 'Hybrid Retrieval-Augmented Generation Pipeline',
    description: 'Hybrid RAG pipeline over ~130 unstructured PDFs + a scraped wiki. LLM-driven semantic chunking, local embeddings, pgvector + HNSW hybrid search, context-window expansion, and query decomposition + grounded answer synthesis. Deployed live in a Minecraft server chat.',
    category: 'ai-data',
    tech: [
      { name: 'PostgreSQL/pgvector', icon: 'logos:postgresql' },
      { name: 'RAG', icon: 'carbon:machine-learning' },
      { name: 'Gemini LLM', icon: 'carbon:ai' },
      { name: 'HNSW Vector Search', icon: 'carbon:data-vis-4' },
      { name: 'TypeScript', icon: 'logos:typescript-icon' }
    ],
    github: 'https://github.com/firatege/RagForGtnh',
    color: 'green'
  },
  {
    id: 6,
    title: 'Deprem Hasar Tespiti',
    subtitle: 'Satellite-Based Earthquake Damage Classification',
    description: 'Binary building-damage classifier over pre/post-disaster satellite image pairs (xView2 dataset). Iterative feature engineering — pixel statistics, SSIM, edge deltas, percentile + quadrant features — took a HistGradientBoostingClassifier from F1 0.70 to 0.78 (ROC-AUC 0.93).',
    category: 'ai-data',
    tech: [
      { name: 'Python', icon: 'logos:python' },
      { name: 'Scikit-learn', icon: 'simple-icons:scikitlearn' },
      { name: 'Computer Vision', icon: 'carbon:image-search' },
      { name: 'Pandas', icon: 'simple-icons:pandas' }
    ],
    github: 'https://github.com/firatege/deprem-hasar-tespiti',
    color: 'purple'
  },
  {
    id: 7,
    title: 'ChatBot',
    subtitle: 'Retrieval-Based NLP Experiment',
    description: 'My first hands-on NLP project: TF-IDF intent classification + POS-tag entity extraction + similarity-based response retrieval from Postgres. Kept as the "before" — no embeddings, no LLM — that motivated the move to real RAG.',
    category: 'ai-data',
    tech: [
      { name: 'Python', icon: 'logos:python' },
      { name: 'PostgreSQL', icon: 'logos:postgresql' },
      { name: 'TF-IDF/NLP', icon: 'carbon:text-link-analysis' }
    ],
    github: 'https://github.com/firatege/ChatBot',
    color: 'cyan'
  },
  {
    id: 8,
    title: 'Envanter Tahmin Platformu',
    subtitle: 'Multi-SKU Demand Forecasting + Order Management',
    description: 'Graduation thesis turned production stack: SKU-level sales forecasting (Prophet + SARIMA + ETS + RF/XGBoost, NNLS stacking, intermittent-demand models) driving MOQ-constrained purchase-order recommendations. Rust API + Python forecast workers + React dashboard on Kubernetes.',
    category: 'ai-data',
    tech: [
      { name: 'Python', icon: 'logos:python' },
      { name: 'Rust', icon: 'logos:rust' },
      { name: 'XGBoost', icon: 'carbon:decision-tree' },
      { name: 'React', icon: 'logos:react' },
      { name: 'PostgreSQL', icon: 'logos:postgresql' }
    ],
    github: 'https://github.com/firatege/Envanter-Tahmin-Platformu',
    color: 'green'
  },
  {
    id: 9,
    title: 'Edu-Rank Prediction',
    subtitle: 'University Ranking Prediction Model',
    description: 'Random Forest model predicting university rankings with 73% accuracy. Features hyperparameter tuning, class balancing, and comprehensive performance metrics across 13 rank categories.',
    category: 'ai-data',
    tech: [
      { name: 'Python', icon: 'logos:python' },
      { name: 'Scikit-learn', icon: 'simple-icons:scikitlearn' },
      { name: 'Random Forest', icon: 'carbon:decision-tree' },
      { name: 'Pandas', icon: 'simple-icons:pandas' }
    ],
    github: 'https://github.com/firatege/edu-rank-prediction',
    color: 'purple'
  },
  {
    id: 10,
    title: 'THE-SCRAPE',
    subtitle: 'University Rankings Auto-Scraper',
    description: 'Automated web scraper for Times Higher Education university rankings. Collects and processes ranking data using Python requests library.',
    category: 'ai-data',
    tech: [
      { name: 'Python', icon: 'logos:python' },
      { name: 'Requests', icon: 'carbon:http' },
      { name: 'Web Scraping', icon: 'carbon:data-collection' },
      { name: 'Data Processing', icon: 'carbon:data-refinery' }
    ],
    github: 'https://github.com/firatege/THE-SCRAPE',
    color: 'green'
  },
  {
    id: 11,
    title: 'Data-Science',
    subtitle: 'ML & Data Science Portfolio',
    description: 'Collection of practical ML examples including time series analysis, data preprocessing, and various machine learning implementations from coursework and personal projects.',
    category: 'ai-data',
    tech: [
      { name: 'Python', icon: 'logos:python' },
      { name: 'Machine Learning', icon: 'carbon:machine-learning' },
      { name: 'Time Series', icon: 'carbon:chart-line' },
      { name: 'Pandas', icon: 'simple-icons:pandas' },
      { name: 'NumPy', icon: 'simple-icons:numpy' }
    ],
    github: 'https://github.com/firatege/Data-Science',
    color: 'cyan'
  },
  // Full Stack Projects
  {
    id: 12,
    title: 'NeuroCanvas',
    subtitle: 'Real-Time Handwritten Digit Recognition',
    description: 'Full-stack demo with browser canvas, Python/TensorFlow model inference, and CNN activation visualization. Rust backend with Kubernetes deployment.',
    category: 'fullstack',
    tech: [
      { name: 'TensorFlow', icon: 'logos:tensorflow' },
      { name: 'Rust', icon: 'logos:rust' },
      { name: 'Actix-Web', icon: 'simple-icons:actix' },
      { name: 'Kubernetes', icon: 'logos:kubernetes' },
      { name: 'Python', icon: 'logos:python' }
    ],
    github: 'https://github.com/firatege/neurocanvas-backend',
    github2: 'https://github.com/firatege/NeuroCanvas-trainer',
    color: 'purple'
  },
  {
    id: 13,
    title: 'GitMyDayTime',
    subtitle: 'Daily Task Tracking PWA',
    description: 'Production task/time-tracking app used daily, deployed at gmd.byfeb.com. Installable PWA, group/project management with a Jira-like board, real-time updates over SSE, activity-log-driven insights, JWT + Redis sessions.',
    category: 'fullstack',
    tech: [
      { name: 'React', icon: 'logos:react' },
      { name: 'TypeScript', icon: 'logos:typescript-icon' },
      { name: 'PostgreSQL', icon: 'logos:postgresql' },
      { name: 'Redis', icon: 'logos:redis' },
      { name: 'Kubernetes', icon: 'logos:kubernetes' }
    ],
    github: 'https://github.com/Auth-ism/GitMyDayTime',
    color: 'cyan'
  }
]

const filteredProjects = ref(projects)

function setFilter(filterId) {
  activeFilter.value = filterId
  if (filterId === 'all') {
    filteredProjects.value = projects
  } else {
    filteredProjects.value = projects.filter(p => p.category === filterId)
  }
}

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

  const section = document.querySelector('.projects-section')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="projects" class="projects-section">
    <!-- Background with bubbles/clusters -->
    <div class="projects-bg">
      <div class="bg-gradient"></div>
      <div class="bg-gradient-2"></div>

      <!-- Floating Bubbles -->
      <div class="bubbles">
        <div class="bubble bubble-1"></div>
        <div class="bubble bubble-2"></div>
        <div class="bubble bubble-3"></div>
        <div class="bubble bubble-4"></div>
        <div class="bubble bubble-5"></div>
        <div class="bubble bubble-6"></div>
        <div class="bubble bubble-7"></div>
        <div class="bubble bubble-8"></div>
        <div class="bubble bubble-9"></div>
        <div class="bubble bubble-10"></div>
        <div class="bubble bubble-11"></div>
        <div class="bubble bubble-12"></div>
      </div>

      <!-- Cluster circles -->
      <svg class="cluster-svg" viewBox="0 0 1000 800" preserveAspectRatio="xMidYMid slice">
        <defs>
          <radialGradient id="bubbleGrad1" cx="50%" cy="50%" r="50%">
            <stop offset="0%" style="stop-color:rgba(34,211,238,0.15)" />
            <stop offset="100%" style="stop-color:rgba(34,211,238,0)" />
          </radialGradient>
          <radialGradient id="bubbleGrad2" cx="50%" cy="50%" r="50%">
            <stop offset="0%" style="stop-color:rgba(16,185,129,0.12)" />
            <stop offset="100%" style="stop-color:rgba(16,185,129,0)" />
          </radialGradient>
          <radialGradient id="bubbleGrad3" cx="50%" cy="50%" r="50%">
            <stop offset="0%" style="stop-color:rgba(139,92,246,0.1)" />
            <stop offset="100%" style="stop-color:rgba(139,92,246,0)" />
          </radialGradient>
        </defs>

        <!-- Cluster 1 - top right -->
        <circle cx="850" cy="150" r="80" fill="url(#bubbleGrad1)" class="cluster-circle c1" />
        <circle cx="900" cy="200" r="50" fill="url(#bubbleGrad2)" class="cluster-circle c2" />
        <circle cx="800" cy="100" r="35" fill="url(#bubbleGrad3)" class="cluster-circle c3" />

        <!-- Cluster 2 - bottom left -->
        <circle cx="100" cy="650" r="70" fill="url(#bubbleGrad2)" class="cluster-circle c4" />
        <circle cx="150" cy="700" r="45" fill="url(#bubbleGrad1)" class="cluster-circle c5" />
        <circle cx="60" cy="600" r="30" fill="url(#bubbleGrad3)" class="cluster-circle c6" />

        <!-- Cluster 3 - center -->
        <circle cx="500" cy="400" r="100" fill="url(#bubbleGrad3)" class="cluster-circle c7" />
        <circle cx="550" cy="350" r="40" fill="url(#bubbleGrad1)" class="cluster-circle c8" />
        <circle cx="450" cy="450" r="55" fill="url(#bubbleGrad2)" class="cluster-circle c9" />
      </svg>
    </div>

    <div class="projects-container" :class="{ 'visible': isVisible }">
      <!-- Section Header -->
      <div class="section-header">
        <span class="section-tag">&lt;projects&gt;</span>
        <h2 class="section-title">Featured Projects</h2>
        <div class="title-underline"></div>
      </div>

      <!-- Filter Tabs -->
      <div class="filter-tabs">
        <button
          v-for="filter in filters"
          :key="filter.id"
          class="filter-btn"
          :class="{ active: activeFilter === filter.id }"
          @click="setFilter(filter.id)"
        >
          {{ filter.label }}
        </button>
      </div>

      <!-- Projects Grid -->
      <div class="projects-grid">
        <div
          v-for="(project, index) in filteredProjects"
          :key="project.id"
          class="project-card"
          :class="[`color-${project.color}`, { 'archived': project.status === 'archived' }]"
          :style="{ animationDelay: `${index * 0.1}s` }"
        >
          <!-- Card Content -->
          <div class="card-content">
            <div class="card-header">
              <div class="folder-icon">
                <Folder :size="36" />
              </div>
              <div class="card-links">
                <a :href="project.github" target="_blank" class="card-link" @click.stop>
                  <Github :size="18" />
                </a>
              </div>
            </div>

            <div class="card-body">
              <h3 class="project-title">{{ project.title }}</h3>
              <p class="project-subtitle">{{ project.subtitle }}</p>

              <div class="project-tech">
                <div v-for="tech in project.tech.slice(0, 4)" :key="tech.name" class="tech-icon" :title="tech.name">
                  <Icon :icon="tech.icon" width="18" height="18" />
                </div>
                <span v-if="project.tech.length > 4" class="tech-more">+{{ project.tech.length - 4 }}</span>
              </div>
            </div>

            <div class="card-footer">
              <span class="category-badge">{{ project.category === 'ai-data' ? 'AI & Data' : project.category === 'fullstack' ? 'Full Stack' : 'Backend' }}</span>
              <span v-if="project.status === 'archived'" class="status-badge archived">Archived</span>
            </div>
          </div>

          <!-- Hover Overlay -->
          <div class="card-overlay">
            <div class="overlay-content">
              <h3 class="overlay-title">{{ project.title }}</h3>
              <p class="overlay-description">{{ project.description }}</p>

              <div class="overlay-tech">
                <span v-for="tech in project.tech" :key="tech.name" class="tech-tag">
                  <Icon :icon="tech.icon" width="12" height="12" />
                  {{ tech.name }}
                </span>
              </div>

              <a :href="project.github" target="_blank" class="github-btn" @click.stop>
                <Github :size="16" />
                <span>View Code</span>
                <ExternalLink :size="12" />
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- Section Footer -->
      <div class="section-footer">
        <span class="section-tag">&lt;/projects&gt;</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects-section {
  min-height: 100vh;
  padding: 6rem 2rem;
  position: relative;
  overflow: hidden;
  background: radial-gradient(ellipse at 50% 50%, #0c1929 0%, #070d15 100%);
}

/* Background */
.projects-bg {
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
  top: 20%;
  right: -10%;
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(139, 92, 246, 0.04) 0%, transparent 70%);
  filter: blur(80px);
}

.bg-gradient-2 {
  position: absolute;
  bottom: 10%;
  left: -10%;
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, rgba(6, 182, 212, 0.04) 0%, transparent 70%);
  filter: blur(80px);
}

/* Floating Bubbles */
.bubbles {
  position: absolute;
  width: 100%;
  height: 100%;
}

.bubble {
  position: absolute;
  border-radius: 50%;
  opacity: 0.06;
  animation: floatBubble 20s ease-in-out infinite;
}

.bubble-1 { width: 120px; height: 120px; top: 10%; left: 5%; background: radial-gradient(circle at 30% 30%, rgba(34,211,238,0.3), transparent); animation-delay: 0s; }
.bubble-2 { width: 80px; height: 80px; top: 25%; right: 10%; background: radial-gradient(circle at 30% 30%, rgba(16,185,129,0.3), transparent); animation-delay: 2s; }
.bubble-3 { width: 60px; height: 60px; top: 60%; left: 15%; background: radial-gradient(circle at 30% 30%, rgba(139,92,246,0.3), transparent); animation-delay: 4s; }
.bubble-4 { width: 100px; height: 100px; top: 70%; right: 20%; background: radial-gradient(circle at 30% 30%, rgba(34,211,238,0.3), transparent); animation-delay: 6s; }
.bubble-5 { width: 50px; height: 50px; top: 40%; left: 40%; background: radial-gradient(circle at 30% 30%, rgba(16,185,129,0.3), transparent); animation-delay: 8s; }
.bubble-6 { width: 70px; height: 70px; top: 85%; left: 30%; background: radial-gradient(circle at 30% 30%, rgba(139,92,246,0.3), transparent); animation-delay: 10s; }
.bubble-7 { width: 90px; height: 90px; top: 15%; left: 60%; background: radial-gradient(circle at 30% 30%, rgba(34,211,238,0.25), transparent); animation-delay: 3s; }
.bubble-8 { width: 40px; height: 40px; top: 50%; right: 5%; background: radial-gradient(circle at 30% 30%, rgba(16,185,129,0.25), transparent); animation-delay: 7s; }
.bubble-9 { width: 55px; height: 55px; top: 30%; left: 25%; background: radial-gradient(circle at 30% 30%, rgba(139,92,246,0.25), transparent); animation-delay: 1s; }
.bubble-10 { width: 85px; height: 85px; bottom: 20%; right: 35%; background: radial-gradient(circle at 30% 30%, rgba(34,211,238,0.25), transparent); animation-delay: 5s; }
.bubble-11 { width: 45px; height: 45px; top: 5%; right: 40%; background: radial-gradient(circle at 30% 30%, rgba(16,185,129,0.25), transparent); animation-delay: 9s; }
.bubble-12 { width: 65px; height: 65px; bottom: 5%; left: 50%; background: radial-gradient(circle at 30% 30%, rgba(139,92,246,0.25), transparent); animation-delay: 11s; }

@keyframes floatBubble {
  0%, 100% { transform: translate(0, 0) scale(1); }
  25% { transform: translate(15px, -20px) scale(1.05); }
  50% { transform: translate(-10px, -35px) scale(1); }
  75% { transform: translate(20px, -15px) scale(0.95); }
}

/* Cluster SVG */
.cluster-svg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.5;
}

.cluster-circle {
  animation: pulseBubble 8s ease-in-out infinite;
}

.c1 { animation-delay: 0s; }
.c2 { animation-delay: 1s; }
.c3 { animation-delay: 2s; }
.c4 { animation-delay: 3s; }
.c5 { animation-delay: 4s; }
.c6 { animation-delay: 5s; }
.c7 { animation-delay: 1.5s; }
.c8 { animation-delay: 2.5s; }
.c9 { animation-delay: 3.5s; }

@keyframes pulseBubble {
  0%, 100% { opacity: 0.3; transform: scale(1); }
  50% { opacity: 0.6; transform: scale(1.1); }
}

/* Container */
.projects-container {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 2;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease-out;
}

.projects-container.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Section Header */
.section-header {
  text-align: center;
  margin-bottom: 3rem;
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

/* Filter Tabs */
.filter-tabs {
  display: flex;
  justify-content: center;
  gap: 0.75rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 0.6rem 1.25rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 25px;
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.9rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-btn:hover {
  background: rgba(255, 255, 255, 0.08);
  color: rgba(255, 255, 255, 0.9);
}

.filter-btn.active {
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.2), rgba(16, 185, 129, 0.2));
  border-color: rgba(34, 211, 238, 0.4);
  color: #22d3ee;
}

/* Projects Grid */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 2rem;
}

/* Project Card */
.project-card {
  position: relative;
  height: 280px;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.08);
  overflow: hidden;
  animation: cardFadeIn 0.5s ease-out forwards;
  opacity: 0;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.project-card:hover {
  transform: translateY(-8px);
  border-color: rgba(34, 211, 238, 0.3);
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.25);
}

.project-card.color-cyan { border-top: 3px solid #22d3ee; }
.project-card.color-green { border-top: 3px solid #10b981; }
.project-card.color-purple { border-top: 3px solid #a78bfa; }

.project-card.archived { opacity: 0.7; }

@keyframes cardFadeIn {
  to { opacity: 1; }
}

/* Card Content */
.card-content {
  padding: 1.5rem;
  height: 100%;
  display: flex;
  flex-direction: column;
  transition: opacity 0.3s ease;
}

.project-card:hover .card-content {
  opacity: 0;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1.25rem;
}

.folder-icon {
  color: rgba(34, 211, 238, 0.6);
}

.project-card.color-green .folder-icon { color: rgba(16, 185, 129, 0.6); }
.project-card.color-purple .folder-icon { color: rgba(167, 139, 250, 0.6); }

.card-links {
  display: flex;
  gap: 0.5rem;
}

.card-link {
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 8px;
  color: rgba(255, 255, 255, 0.5);
  transition: all 0.2s ease;
}

.card-link:hover {
  background: rgba(34, 211, 238, 0.2);
  color: #22d3ee;
}

.card-body {
  flex: 1;
}

.project-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 0.4rem;
}

.project-subtitle {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.5);
  margin-bottom: 1rem;
  line-height: 1.4;
}

.project-tech {
  display: flex;
  align-items: center;
  gap: 0.4rem;
}

.tech-icon {
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 6px;
  color: rgba(255, 255, 255, 0.7);
}

.tech-more {
  font-size: 0.7rem;
  color: rgba(255, 255, 255, 0.4);
  margin-left: 0.25rem;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
}

.category-badge {
  font-size: 0.65rem;
  padding: 0.2rem 0.5rem;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 10px;
  color: rgba(255, 255, 255, 0.5);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.status-badge.archived {
  font-size: 0.6rem;
  padding: 0.15rem 0.4rem;
  background: rgba(239, 68, 68, 0.15);
  border-radius: 8px;
  color: #f87171;
  text-transform: uppercase;
}

/* Hover Overlay */
.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.95), rgba(16, 185, 129, 0.95));
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.project-card.color-green .card-overlay {
  background: linear-gradient(135deg, rgba(16, 185, 129, 0.95), rgba(6, 182, 212, 0.95));
}

.project-card.color-purple .card-overlay {
  background: linear-gradient(135deg, rgba(139, 92, 246, 0.95), rgba(6, 182, 212, 0.95));
}

.project-card:hover .card-overlay {
  opacity: 1;
  transform: translateY(0);
}

.overlay-content {
  display: flex;
  flex-direction: column;
  height: 100%;
}

.overlay-title {
  font-size: 1.2rem;
  font-weight: 700;
  color: white;
  margin-bottom: 0.75rem;
}

.overlay-description {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.9);
  line-height: 1.6;
  margin-bottom: 1rem;
  flex: 1;
  min-height: 0;
  overflow-y: auto;
  scrollbar-width: thin;
  scrollbar-color: rgba(255, 255, 255, 0.4) transparent;
}

.overlay-description::-webkit-scrollbar {
  width: 4px;
}

.overlay-description::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.4);
  border-radius: 2px;
}

.overlay-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.35rem;
  margin-bottom: 1rem;
  flex-shrink: 0;
}

.tech-tag {
  display: flex;
  align-items: center;
  gap: 0.25rem;
  font-size: 0.65rem;
  padding: 0.2rem 0.45rem;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 5px;
  color: white;
}

.github-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.65rem 1rem;
  background: rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 10px;
  color: white;
  font-size: 0.8rem;
  font-weight: 500;
  text-decoration: none;
  transition: all 0.2s ease;
  margin-top: auto;
  flex-shrink: 0;
}

.github-btn:hover {
  background: rgba(0, 0, 0, 0.3);
  border-color: rgba(255, 255, 255, 0.5);
}

/* Section Footer */
.section-footer {
  text-align: center;
  margin-top: 4rem;
}

/* Responsive */
@media (max-width: 900px) {
  .projects-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .projects-section {
    padding: 4rem 1.5rem;
  }

  .section-title {
    font-size: clamp(2rem, 6vw, 2.5rem);
  }

  .projects-grid {
    grid-template-columns: 1fr;
    gap: 1.25rem;
  }

  .project-card {
    height: 280px;
  }

  .filter-tabs {
    flex-wrap: wrap;
    justify-content: center;
    gap: 0.5rem;
  }

  .filter-btn {
    padding: 0.6rem 1rem;
    font-size: 0.85rem;
  }

  /* On mobile, show overlay by default since hover doesn't work well */
  .project-card .card-overlay {
    opacity: 0;
    pointer-events: none;
  }

  .project-card:active .card-overlay {
    opacity: 1;
    pointer-events: auto;
    transform: translateY(0);
  }

  .folder-icon svg {
    width: 28px;
    height: 28px;
  }

  .project-title {
    font-size: 1.1rem;
  }

  .project-subtitle {
    font-size: 0.8rem;
  }
}

@media (max-width: 640px) {
  .projects-section {
    padding: 3rem 1rem;
  }

  .project-card {
    height: 260px;
    border-radius: 12px;
  }

  .card-content {
    padding: 1.25rem;
  }

  .card-header {
    margin-bottom: 1rem;
  }

  .folder-icon svg {
    width: 24px;
    height: 24px;
  }

  .card-link {
    width: 28px;
    height: 28px;
  }

  .project-title {
    font-size: 1rem;
  }

  .project-subtitle {
    font-size: 0.75rem;
    margin-bottom: 0.75rem;
  }

  .tech-icon {
    width: 26px;
    height: 26px;
  }

  .category-badge {
    font-size: 0.6rem;
  }

  .card-overlay {
    padding: 1.25rem;
  }

  .overlay-title {
    font-size: 1rem;
  }

  .overlay-description {
    font-size: 0.75rem;
  }

  .overlay-tech {
    gap: 0.25rem;
  }

  .tech-tag {
    font-size: 0.6rem;
    padding: 0.15rem 0.35rem;
  }

  .github-btn {
    padding: 0.5rem 0.75rem;
    font-size: 0.75rem;
  }
}

@media (max-width: 480px) {
  .projects-section {
    padding: 2.5rem 0.75rem;
  }

  .section-header {
    margin-bottom: 1.5rem;
  }

  .section-tag {
    font-size: 0.85rem;
  }

  .filter-tabs {
    gap: 0.4rem;
  }

  .filter-btn {
    padding: 0.5rem 0.75rem;
    font-size: 0.8rem;
    border-radius: 8px;
  }

  .projects-grid {
    gap: 1rem;
  }

  .project-card {
    height: 240px;
  }

  .card-content {
    padding: 1rem;
  }

  .project-title {
    font-size: 0.95rem;
  }

  .project-subtitle {
    font-size: 0.7rem;
    line-height: 1.4;
  }

  .tech-icon {
    width: 24px;
    height: 24px;
    border-radius: 4px;
  }

  .section-footer {
    margin-top: 2rem;
  }
}
</style>
