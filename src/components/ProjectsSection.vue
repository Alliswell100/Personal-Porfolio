<template>
  <section id="projects" class="section projects">
    <div class="container">
      <div class="section-header fade-in">
        <h2 class="section-title">Featured Projects</h2>
        <p class="section-subtitle">A showcase of my recent work and creative solutions</p>
      </div>
      
      <div class="projects-grid">
        <div class="project-card fade-in" v-for="project in projects" :key="project.id">
          <div class="project-image">
            <img :src="project.image" :alt="project.title" />
            <div class="project-overlay">
              <div class="project-actions">
                <a :href="project.demo" class="btn btn-primary" target="_blank">Live Demo</a>
                <a :href="project.github" class="btn" target="_blank">Code</a>
              </div>
            </div>
          </div>
          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            <div class="project-tech">
              <span class="tech-tag" v-for="tech in project.technologies" :key="tech">
                {{ tech }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const projects = ref([
  {
    id: 1,
    title: 'E-Commerce Platform',
    description: 'Full-stack e-commerce solution with React, Node.js, and Stripe integration. Features include user authentication, product management, and secure payments.',
    image: 'https://images.pexels.com/photos/230544/pexels-photo-230544.jpeg?auto=compress&cs=tinysrgb&w=800',
    demo: '#',
    github: '#',
    technologies: ['React', 'Node.js', 'MongoDB', 'Stripe']
  },
  {
    id: 2,
    title: 'Task Management App',
    description: 'Collaborative task management application with real-time updates, drag-and-drop functionality, and team collaboration features.',
    image: 'https://images.pexels.com/photos/7688336/pexels-photo-7688336.jpeg?auto=compress&cs=tinysrgb&w=800',
    demo: '#',
    github: '#',
    technologies: ['Vue.js', 'Socket.io', 'Express', 'PostgreSQL']
  },
  {
    id: 3,
    title: 'Weather Dashboard',
    description: 'Beautiful weather application with location-based forecasts, interactive maps, and customizable widgets for weather tracking.',
    image: 'https://images.pexels.com/photos/1118873/pexels-photo-1118873.jpeg?auto=compress&cs=tinysrgb&w=800',
    demo: '#',
    github: '#',
    technologies: ['TypeScript', 'Chart.js', 'OpenWeather API', 'PWA']
  },
  {
    id: 4,
    title: 'Social Media Analytics',
    description: 'Comprehensive analytics dashboard for social media management with data visualization and automated reporting features.',
    image: 'https://images.pexels.com/photos/590020/pexels-photo-590020.jpg?auto=compress&cs=tinysrgb&w=800',
    demo: '#',
    github: '#',
    technologies: ['Python', 'Django', 'D3.js', 'Redis']
  },
  {
    id: 5,
    title: 'Recipe Sharing Platform',
    description: 'Community-driven recipe sharing platform with search functionality, user reviews, and meal planning features.',
    image: 'https://images.pexels.com/photos/1640777/pexels-photo-1640777.jpeg?auto=compress&cs=tinysrgb&w=800',
    demo: '#',
    github: '#',
    technologies: ['Next.js', 'Prisma', 'Supabase', 'Tailwind']
  },
  {
    id: 6,
    title: 'Fitness Tracker',
    description: 'Personal fitness tracking application with workout logging, progress visualization, and goal setting capabilities.',
    image: 'https://images.pexels.com/photos/4162493/pexels-photo-4162493.jpeg?auto=compress&cs=tinysrgb&w=800',
    demo: '#',
    github: '#',
    technologies: ['React Native', 'Firebase', 'Chart.js', 'AsyncStorage']
  }
])

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
      }
    })
  }, { threshold: 0.1 })
  
  document.querySelectorAll('.fade-in').forEach((el) => {
    observer.observe(el)
  })
})
</script>

<style scoped>
.projects {
  background: #0a0a0a;
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

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
}

.project-card {
  background: rgba(26, 26, 26, 0.5);
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid #333;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.project-card:hover {
  transform: translateY(-8px);
  border-color: #444;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

.project-image {
  position: relative;
  overflow: hidden;
  aspect-ratio: 16/10;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.project-actions {
  display: flex;
  gap: 1rem;
}

.project-content {
  padding: 1.5rem;
}

.project-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: #f5f5f5;
  margin-bottom: 0.75rem;
}

.project-description {
  color: #bbb;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-tag {
  background: rgba(102, 102, 102, 0.2);
  color: #ccc;
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.875rem;
  border: 1px solid #444;
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .project-actions {
    flex-direction: column;
    align-items: center;
  }
  
  .btn {
    width: 120px;
    justify-content: center;
  }
}

@media (max-width: 1200px) {
  .projects-grid {
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 1.75rem;
  }
}

@media (max-width: 992px) {
  .section-title {
    font-size: clamp(1.75rem, 3.5vw, 2.5rem);
  }
  
  .section-subtitle {
    font-size: 1rem;
  }
  
  .projects-grid {
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  }
  
  .project-content {
    padding: 1.25rem;
  }
  
  .project-title {
    font-size: 1.125rem;
  }
  
  .project-description {
    font-size: 0.95rem;
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
  
  .projects-grid {
    grid-template-columns: 1fr;
    gap: 1.25rem;
  }
  
  .project-card {
    border-radius: 10px;
  }
  
  .project-content {
    padding: 1rem;
  }
  
  .project-title {
    font-size: 1rem;
    margin-bottom: 0.5rem;
  }
  
  .project-description {
    font-size: 0.9rem;
    margin-bottom: 0.75rem;
    line-height: 1.5;
  }
  
  .project-actions {
    gap: 0.75rem;
  }
  
  .btn {
    width: 100px;
    padding: 0.5rem 0.75rem;
    font-size: 0.8rem;
  }
  
  .tech-tag {
    padding: 0.2rem 0.6rem;
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .section-header {
    margin-bottom: 2.5rem;
  }
  
  .project-image {
    aspect-ratio: 16/9;
  }
  
  .project-content {
    padding: 0.875rem;
  }
  
  .project-title {
    font-size: 0.95rem;
  }
  
  .project-description {
    font-size: 0.85rem;
  }
  
  .project-actions {
    gap: 0.5rem;
  }
  
  .btn {
    width: 90px;
    padding: 0.45rem 0.5rem;
    font-size: 0.75rem;
  }
  
  .tech-tag {
    padding: 0.15rem 0.5rem;
    font-size: 0.75rem;
  }
}

@media (max-width: 360px) {
  .project-content {
    padding: 0.75rem;
  }
  
  .project-title {
    font-size: 0.9rem;
  }
  
  .project-description {
    font-size: 0.8rem;
  }
  
  .project-tech {
    gap: 0.375rem;
  }
  
  .tech-tag {
    padding: 0.125rem 0.4rem;
    font-size: 0.7rem;
  }
}
</style>