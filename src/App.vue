<script setup>
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'
import BadAppleBg from './components/BadAppleBg.vue'
</script>

<template>
  <div class="app">
    <NavBar />
    <BadAppleBg />
    <HeroSection />
    <AboutSection />
    <SkillsSection />
    <ExperienceSection />
    <ProjectsSection />
    <ContactSection />
    <FooterSection />
  </div>
</template>

<style scoped>
.app {
  min-height: 100vh;
  overflow-x: hidden;
  background: #070d15;
}
</style>
