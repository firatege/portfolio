<script setup>
import { ref, onMounted } from 'vue'
import { Mail, MapPin, Send, Github, Linkedin, Twitter } from 'lucide-vue-next'

const isVisible = ref(false)

const socialLinks = [
  { name: 'GitHub', icon: Github, url: 'https://github.com/firatege', color: '#22d3ee' },
  { name: 'LinkedIn', icon: Linkedin, url: 'https://www.linkedin.com/in/byfeb', color: '#10b981' },
  { name: 'X', icon: Twitter, url: 'https://x.com/FratEgeBayram1', color: '#a78bfa' }
]

const form = ref({
  name: '',
  email: '',
  message: ''
})

const isSubmitting = ref(false)
const submitStatus = ref('')

async function handleSubmit() {
  isSubmitting.value = true
  // Simulate form submission
  await new Promise(resolve => setTimeout(resolve, 1500))
  submitStatus.value = 'success'
  isSubmitting.value = false
  form.value = { name: '', email: '', message: '' }

  setTimeout(() => {
    submitStatus.value = ''
  }, 3000)
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

  const section = document.querySelector('.contact-section')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="contact" class="contact-section">
    <!-- Background -->
    <div class="contact-bg">
      <div class="bg-gradient"></div>
      <div class="bg-gradient-2"></div>
      <div class="grid-pattern"></div>
    </div>

    <div class="contact-container" :class="{ 'visible': isVisible }">
      <!-- Section Header -->
      <div class="section-header">
        <span class="section-tag">&lt;contact&gt;</span>
        <h2 class="section-title">Get In Touch</h2>
        <div class="title-underline"></div>
        <p class="section-subtitle">
          Have a project in mind or just want to say hello? Feel free to reach out!
        </p>
      </div>

      <div class="contact-content">
        <!-- Contact Info -->
        <div class="contact-info">
          <div class="info-card">
            <div class="info-icon">
              <Mail :size="24" />
            </div>
            <div class="info-text">
              <h3>Email</h3>
              <a href="mailto:firategebayram@gmail.com">firategebayram@gmail.com</a>
            </div>
          </div>

          <div class="info-card">
            <div class="info-icon location">
              <MapPin :size="24" />
            </div>
            <div class="info-text">
              <h3>Location</h3>
              <span>İzmir, Turkey</span>
            </div>
          </div>

          <!-- Social Links -->
          <div class="social-links">
            <h3>Connect with me</h3>
            <div class="social-icons">
              <a
                v-for="social in socialLinks"
                :key="social.name"
                :href="social.url"
                target="_blank"
                class="social-icon"
                :style="{ '--hover-color': social.color }"
                :title="social.name"
              >
                <component :is="social.icon" :size="22" />
              </a>
            </div>
          </div>
        </div>

        <!-- Contact Form -->
        <form class="contact-form" @submit.prevent="handleSubmit">
          <div class="form-group">
            <label for="name">Name</label>
            <input
              type="text"
              id="name"
              v-model="form.name"
              placeholder="Your name"
              required
            />
          </div>

          <div class="form-group">
            <label for="email">Email</label>
            <input
              type="email"
              id="email"
              v-model="form.email"
              placeholder="your@email.com"
              required
            />
          </div>

          <div class="form-group">
            <label for="message">Message</label>
            <textarea
              id="message"
              v-model="form.message"
              placeholder="Your message..."
              rows="5"
              required
            ></textarea>
          </div>

          <button
            type="submit"
            class="submit-btn"
            :disabled="isSubmitting"
            :class="{ 'success': submitStatus === 'success' }"
          >
            <span v-if="isSubmitting">Sending...</span>
            <span v-else-if="submitStatus === 'success'">Message Sent!</span>
            <span v-else>
              Send Message
              <Send :size="18" />
            </span>
          </button>
        </form>
      </div>

      <!-- Section Footer -->
      <div class="section-footer">
        <span class="section-tag">&lt;/contact&gt;</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact-section {
  min-height: 100vh;
  padding: 6rem 2rem;
  position: relative;
  overflow: hidden;
  background: radial-gradient(ellipse at 50% 50%, #0c1929 0%, #070d15 100%);
}

/* Background */
.contact-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

.bg-gradient {
  position: absolute;
  top: 20%;
  left: -10%;
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, rgba(6, 182, 212, 0.06) 0%, transparent 70%);
  filter: blur(80px);
}

.bg-gradient-2 {
  position: absolute;
  bottom: 10%;
  right: -10%;
  width: 400px;
  height: 400px;
  background: radial-gradient(circle, rgba(16, 185, 129, 0.05) 0%, transparent 70%);
  filter: blur(80px);
}

.grid-pattern {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image:
    linear-gradient(rgba(34, 211, 238, 0.02) 1px, transparent 1px),
    linear-gradient(90deg, rgba(34, 211, 238, 0.02) 1px, transparent 1px);
  background-size: 50px 50px;
  opacity: 0.5;
}

/* Container */
.contact-container {
  max-width: 1000px;
  margin: 0 auto;
  position: relative;
  z-index: 2;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease-out;
}

.contact-container.visible {
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
  margin: 0 auto 1.5rem;
  border-radius: 2px;
}

.section-subtitle {
  font-size: 1.1rem;
  color: rgba(255, 255, 255, 0.6);
  max-width: 500px;
  margin: 0 auto;
}

/* Content Layout */
.contact-content {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 3rem;
  align-items: start;
}

/* Contact Info */
.contact-info {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.info-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.25rem;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 12px;
  transition: all 0.3s ease;
}

.info-card:hover {
  background: rgba(255, 255, 255, 0.04);
  border-color: rgba(34, 211, 238, 0.2);
  transform: translateX(5px);
}

.info-icon {
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(34, 211, 238, 0.1);
  border-radius: 12px;
  color: #22d3ee;
}

.info-icon.location {
  background: rgba(16, 185, 129, 0.1);
  color: #10b981;
}

.info-text h3 {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.5);
  margin-bottom: 0.25rem;
  font-weight: 500;
}

.info-text a,
.info-text span {
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.9);
  text-decoration: none;
  transition: color 0.2s ease;
}

.info-text a:hover {
  color: #22d3ee;
}

/* Social Links */
.social-links {
  margin-top: 1rem;
}

.social-links h3 {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.5);
  margin-bottom: 1rem;
  font-weight: 500;
}

.social-icons {
  display: flex;
  gap: 0.75rem;
}

.social-icon {
  width: 45px;
  height: 45px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  color: rgba(255, 255, 255, 0.7);
  transition: all 0.3s ease;
}

.social-icon:hover {
  background: rgba(255, 255, 255, 0.08);
  border-color: #22d3ee;
  color: #22d3ee;
  transform: translateY(-3px);
}

/* Contact Form */
.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
  font-weight: 500;
}

.form-group input,
.form-group textarea {
  padding: 0.875rem 1rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  color: white;
  font-size: 1rem;
  font-family: inherit;
  transition: all 0.2s ease;
  resize: none;
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: rgba(255, 255, 255, 0.3);
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: rgba(34, 211, 238, 0.5);
  background: rgba(255, 255, 255, 0.05);
}

.submit-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 1rem 2rem;
  background: linear-gradient(135deg, #06b6d4, #10b981);
  border: none;
  border-radius: 10px;
  color: white;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-top: 0.5rem;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(6, 182, 212, 0.3);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.submit-btn.success {
  background: linear-gradient(135deg, #10b981, #059669);
}

/* Section Footer */
.section-footer {
  text-align: center;
  margin-top: 4rem;
}

/* Responsive */
@media (max-width: 768px) {
  .contact-section {
    padding: 4rem 1.5rem;
  }

  .section-title {
    font-size: clamp(2rem, 6vw, 2.5rem);
  }

  .section-subtitle {
    font-size: 1rem;
    padding: 0 1rem;
  }

  .contact-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .contact-info {
    order: 2;
    gap: 1.25rem;
  }

  .contact-form {
    order: 1;
    padding: 1.5rem;
  }

  .info-card {
    padding: 1rem;
  }

  .social-links h3 {
    text-align: center;
  }

  .social-icons {
    justify-content: center;
  }
}

@media (max-width: 640px) {
  .contact-section {
    padding: 3rem 1rem;
  }

  .section-header {
    margin-bottom: 2.5rem;
  }

  .contact-form {
    padding: 1.25rem;
    border-radius: 12px;
  }

  .form-group {
    gap: 0.4rem;
  }

  .form-group label {
    font-size: 0.85rem;
  }

  .form-group input,
  .form-group textarea {
    padding: 0.75rem 0.875rem;
    font-size: 0.95rem;
    border-radius: 8px;
  }

  .submit-btn {
    padding: 0.875rem 1.5rem;
    font-size: 0.95rem;
    border-radius: 8px;
  }

  .info-card {
    gap: 0.875rem;
    padding: 0.875rem;
    border-radius: 10px;
  }

  .info-icon {
    width: 40px;
    height: 40px;
  }

  .info-text h3 {
    font-size: 0.85rem;
  }

  .info-text a,
  .info-text span {
    font-size: 0.9rem;
  }

  .social-icon {
    width: 42px;
    height: 42px;
    border-radius: 10px;
  }
}

@media (max-width: 480px) {
  .contact-section {
    padding: 2.5rem 0.75rem;
  }

  .section-tag {
    font-size: 0.85rem;
  }

  .section-subtitle {
    font-size: 0.9rem;
  }

  .contact-form {
    padding: 1rem;
    gap: 1rem;
  }

  .form-group label {
    font-size: 0.8rem;
  }

  .form-group input,
  .form-group textarea {
    padding: 0.7rem 0.75rem;
    font-size: 0.9rem;
  }

  .submit-btn {
    padding: 0.75rem 1.25rem;
    font-size: 0.9rem;
  }

  .info-card {
    padding: 0.75rem;
  }

  .info-icon {
    width: 36px;
    height: 36px;
    border-radius: 8px;
  }

  .info-icon svg {
    width: 18px;
    height: 18px;
  }

  .info-text h3 {
    font-size: 0.8rem;
  }

  .info-text a,
  .info-text span {
    font-size: 0.85rem;
  }

  .social-links h3 {
    font-size: 0.85rem;
  }

  .social-icon {
    width: 40px;
    height: 40px;
  }

  .section-footer {
    margin-top: 2.5rem;
  }
}
</style>
