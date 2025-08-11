<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-section">
          <h3 class="footer-title">John Doe</h3>
          <p class="footer-description">
            Passionate developer creating digital experiences that make a difference.
          </p>
        </div>
        
        <div class="footer-section">
          <h4>Quick Links</h4>
          <ul class="footer-links">
            <li><a href="#home">Home</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </div>
        
        <div class="footer-section">
          <h4>Connect</h4>
          <ul class="footer-links">
            <li><a href="#" target="_blank">LinkedIn</a></li>
            <li><a href="#" target="_blank">GitHub</a></li>
            <li><a href="#" target="_blank">Twitter</a></li>
            <li><a href="#" target="_blank">Email</a></li>
          </ul>
        </div>
      </div>
      
      <div class="footer-bottom">
        <p>&copy; {{ currentYear }} Samuel Godwin. All rights reserved.</p>
        <p>Built with Vue.js and lots of ☕</p>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const currentYear = computed(() => new Date().getFullYear())
</script>

<style scoped>
.footer {
  background: #0a0a0a;
  border-top: 1px solid #333;
  padding: 3rem 0 1rem;
}

.footer-content {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 3rem;
  margin-bottom: 2rem;
}

.footer-section h3,
.footer-section h4 {
  color: #f5f5f5;
  margin-bottom: 1rem;
  font-weight: 600;
}

.footer-title {
  font-size: 1.5rem;
  background: linear-gradient(135deg, #f5f5f5 0%, #999 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.footer-description {
  color: #bbb;
  line-height: 1.6;
  max-width: 300px;
}

.footer-links {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.footer-links a {
  color: #bbb;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-links a:hover {
  color: #f5f5f5;
}

.footer-bottom {
  padding-top: 2rem;
  border-top: 1px solid #333;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #888;
  font-size: 0.875rem;
}

@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
    gap: 2rem;
    text-align: center;
  }
  
  .footer-bottom {
    flex-direction: column;
    gap: 0.5rem;
    text-align: center;
  }
}

@media (max-width: 992px) {
  .footer {
    padding: 2.5rem 0 1rem;
  }
  
  .footer-content {
    gap: 2.5rem;
    margin-bottom: 1.75rem;
  }
  
  .footer-title {
    font-size: 1.375rem;
  }
  
  .footer-description {
    font-size: 0.95rem;
  }
}

@media (max-width: 576px) {
  .footer {
    padding: 2rem 0 0.75rem;
  }
  
  .footer-content {
    gap: 1.75rem;
    margin-bottom: 1.5rem;
  }
  
  .footer-title {
    font-size: 1.25rem;
    margin-bottom: 0.75rem;
  }
  
  .footer-description {
    font-size: 0.9rem;
    max-width: 280px;
    margin: 0 auto;
  }
  
  .footer-section h4 {
    font-size: 1rem;
    margin-bottom: 0.75rem;
  }
  
  .footer-links {
    gap: 0.375rem;
  }
  
  .footer-links a {
    font-size: 0.9rem;
  }
  
  .footer-bottom {
    padding-top: 1.5rem;
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .footer {
    padding: 1.75rem 0 0.5rem;
  }
  
  .footer-content {
    gap: 1.5rem;
    margin-bottom: 1.25rem;
  }
  
  .footer-title {
    font-size: 1.125rem;
  }
  
  .footer-description {
    font-size: 0.85rem;
    max-width: 260px;
  }
  
  .footer-section h4 {
    font-size: 0.95rem;
  }
  
  .footer-links a {
    font-size: 0.85rem;
  }
  
  .footer-bottom {
    padding-top: 1.25rem;
    font-size: 0.75rem;
    gap: 0.375rem;
  }
}

@media (max-width: 360px) {
  .footer {
    padding: 1.5rem 0 0.5rem;
  }
  
  .footer-content {
    gap: 1.25rem;
    margin-bottom: 1rem;
  }
  
  .footer-title {
    font-size: 1rem;
  }
  
  .footer-description {
    font-size: 0.8rem;
    max-width: 240px;
  }
  
  .footer-section h4 {
    font-size: 0.9rem;
    margin-bottom: 0.5rem;
  }
  
  .footer-links {
    gap: 0.25rem;
  }
  
  .footer-links a {
    font-size: 0.8rem;
  }
  
  .footer-bottom {
    padding-top: 1rem;
    font-size: 0.7rem;
  }
}
</style>