<template>
  <section id="about" class="section about">
    <div class="container">
      <div class="section-header fade-in">
        <h2 class="section-title">About Me</h2>
        <p class="section-subtitle">Passionate developer with a love for creating amazing experiences</p>
      </div>
      
      <div class="about-content">
        <div class="about-text fade-in">
          <p>
            I'm a passionate Frontend developer with over 2 years of experience creating 
            digital solutions that make a difference. I specialize in modern web technologies 
            and love turning complex problems into simple, beautiful designs.
          </p>
          <p>
            When I'm not coding, you'll find me exploring new technologies, contributing to 
            open-source projects, or sharing knowledge with the developer community.
          </p>
        </div>
        
        <div class="skills-grid fade-in">
          <div class="skill-category">
            <h3>Frontend</h3>
            <div class="skills">
              <div class="skill" v-for="skill in frontendSkills" :key="skill.name">
                <div class="skill-info">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div class="skill-progress" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
          
          <div class="skill-category">
            <h3>Backend</h3>
            <div class="skills">
              <div class="skill" v-for="skill in backendSkills" :key="skill.name">
                <div class="skill-info">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div class="skill-progress" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
          
          <div class="skill-category">
            <h3>Tools & Others</h3>
            <div class="skills">
              <div class="skill" v-for="skill in toolsSkills" :key="skill.name">
                <div class="skill-info">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-percentage">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div class="skill-progress" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const frontendSkills = ref([
  { name: 'Vue.js', level: 95 },
  { name: 'TypeScript', level: 88 },
  { name: 'CSS/SCSS', level: 92 }
])

const backendSkills = ref([
  { name: 'Node.js', level: 85 },
  { name: 'Python', level: 80 },
])

const toolsSkills = ref([
  { name: 'Git', level: 90 },
  { name: 'AWS', level: 70 },
  { name: 'Figma', level: 85 }
])

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
        
        // Animate skill bars
        if (entry.target.classList.contains('skills-grid')) {
          setTimeout(() => {
            const skillBars = entry.target.querySelectorAll('.skill-progress')
            skillBars.forEach((bar: Element) => {
              const htmlBar = bar as HTMLElement
              htmlBar.style.animation = 'fillBar 1.5s ease-out forwards'
            })
          }, 300)
        }
      }
    })
  }, { threshold: 0.3 })
  
  document.querySelectorAll('.fade-in').forEach((el) => {
    observer.observe(el)
  })
})
</script>

<style scoped>
.about {
  background: linear-gradient(135deg, #0f0f0f 0%, #1a1a1a 100%);
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 700;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #f5f5f5 0%, #999 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  font-size: 1.125rem;
  color: #bbb;
  max-width: 600px;
  margin: 0 auto;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 4rem;
  align-items: start;
}

.about-text {
  font-size: 1.125rem;
  line-height: 1.8;
  color: #ccc;
}

.about-text p {
  margin-bottom: 1.5rem;
}

.skills-grid {
  display: grid;
  gap: 2rem;
}

.skill-category h3 {
  font-size: 1.25rem;
  color: #f5f5f5;
  margin-bottom: 1rem;
  font-weight: 600;
}

.skills {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.skill {
  background: rgba(26, 26, 26, 0.5);
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #333;
  transition: all 0.3s ease;
}

.skill:hover {
  background: rgba(26, 26, 26, 0.8);
  border-color: #444;
  transform: translateY(-2px);
}

.skill-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.skill-name {
  font-weight: 500;
  color: #f5f5f5;
}

.skill-percentage {
  font-size: 0.875rem;
  color: #999;
}

.skill-bar {
  height: 4px;
  background: #333;
  border-radius: 2px;
  overflow: hidden;
}

.skill-progress {
  height: 100%;
  background: linear-gradient(135deg, #666 0%, #888 100%);
  border-radius: 2px;
  width: 0;
  transition: width 1.5s ease-out;
}

@keyframes fillBar {
  from { width: 0; }
  to { width: var(--target-width); }
}

@media (max-width: 968px) {
  .about-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}

@media (max-width: 768px) {
  .skills-grid {
    gap: 1.5rem;
  }
  
  .skill-category h3 {
    font-size: 1.125rem;
  }
}

@media (max-width: 992px) {
  .section-title {
    font-size: clamp(1.75rem, 3.5vw, 2.5rem);
  }
  
  .section-subtitle {
    font-size: 1rem;
  }
  
  .about-text {
    font-size: 1rem;
  }
}

@media (max-width: 576px) {
  .section-header {
    margin-bottom: 3rem;
  }
  
  .section-title {
    font-size: clamp(1.5rem, 5vw, 2.25rem);
    margin-bottom: 0.75rem;
  }
  
  .section-subtitle {
    font-size: 0.95rem;
  }
  
  .about-content {
    gap: 2.5rem;
  }
  
  .about-text {
    font-size: 0.95rem;
    line-height: 1.7;
  }
  
  .about-text p {
    margin-bottom: 1.25rem;
  }
  
  .skills-grid {
    gap: 1.25rem;
  }
  
  .skill {
    padding: 0.875rem;
  }
  
  .skill-category h3 {
    font-size: 1rem;
    margin-bottom: 0.75rem;
  }
  
  .skill-name {
    font-size: 0.9rem;
  }
  
  .skill-percentage {
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .section-header {
    margin-bottom: 2.5rem;
  }
  
  .about-content {
    gap: 2rem;
  }
  
  .about-text {
    font-size: 0.9rem;
  }
  
  .skill {
    padding: 0.75rem;
  }
  
  .skill-info {
    margin-bottom: 0.375rem;
  }
  
  .skill-bar {
    height: 3px;
  }
}

@media (max-width: 360px) {
  .about-text p {
    margin-bottom: 1rem;
  }
  
  .skills-grid {
    gap: 1rem;
  }
  
  .skill {
    padding: 0.625rem;
  }
  
  .skill-category h3 {
    font-size: 0.95rem;
  }
  
  .skill-name {
    font-size: 0.85rem;
  }
  
  .skill-percentage {
    font-size: 0.75rem;
  }
}
</style>