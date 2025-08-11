<template>
  <div id="app">
    <AppHeader />
    <main>
      <HeroSection />
      <AboutSection />
      <ProjectsSection />
      <ContactSection />
    </main>
    <AppFooter />
  </div>
</template>

<script setup lang="ts">
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  background-color: #0a0a0a;
  color: #f5f5f5;
  line-height: 1.6;
  overflow-x: hidden;
}

#app {
  min-height: 100vh;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section {
  padding: 5rem 0;
  position: relative;
}

.fade-in {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 2rem;
  background: linear-gradient(135deg, #333 0%, #555 100%);
  color: #f5f5f5;
  text-decoration: none;
  border-radius: 50px;
  font-weight: 500;
  transition: all 0.3s ease;
  border: 1px solid #444;
  cursor: pointer;
  font-size: 0.95rem;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(85, 85, 85, 0.3);
  background: linear-gradient(135deg, #444 0%, #666 100%);
}

.btn-primary {
  background: linear-gradient(135deg, #666 0%, #888 100%);
  border-color: #777;
}

.btn-primary:hover {
  background: linear-gradient(135deg, #777 0%, #999 100%);
  box-shadow: 0 10px 25px rgba(136, 136, 136, 0.3);
}

/* Media Queries for all screen sizes */
@media (max-width: 1400px) {
  .container {
    max-width: 1000px;
  }
}

@media (max-width: 1200px) {
  .container {
    max-width: 900px;
    padding: 0 1.5rem;
  }
  
  .section {
    padding: 4rem 0;
  }
}

@media (max-width: 992px) {
  .container {
    max-width: 750px;
  }
  
  .section {
    padding: 3.5rem 0;
  }
  
  .btn {
    padding: 0.65rem 1.5rem;
    font-size: 0.9rem;
  }
}

@media (max-width: 768px) {
  .container {
    padding: 0 1rem;
  }
  
  .section {
    padding: 3rem 0;
  }
  
  .btn {
    padding: 0.6rem 1.25rem;
    font-size: 0.875rem;
  }
}

@media (max-width: 576px) {
  .container {
    padding: 0 0.75rem;
  }
  
  .section {
    padding: 2.5rem 0;
  }
  
  .btn {
    padding: 0.55rem 1rem;
    font-size: 0.85rem;
    min-width: 120px;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 0.5rem;
  }
  
  .section {
    padding: 2rem 0;
  }
}

@media (max-width: 360px) {
  .container {
    padding: 0 0.25rem;
  }
  
  .btn {
    padding: 0.5rem 0.75rem;
    font-size: 0.8rem;
    min-width: 100px;
  }
}
</style>