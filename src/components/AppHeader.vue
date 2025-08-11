<template>
  <header class="header" :class="{ 'scrolled': isScrolled }">
    <div class="container">
      <nav class="nav">
        <div class="logo">
          <span class="logo-text">Portfolio</span>
        </div>
        <ul class="nav-menu" :class="{ 'active': isMenuOpen }">
          <li><a href="#home" @click="closeMenu">Home</a></li>
          <li><a href="#about" @click="closeMenu">About</a></li>
          <li><a href="#projects" @click="closeMenu">Projects</a></li>
          <li><a href="#contact" @click="closeMenu">Contact</a></li>
        </ul>
        <button class="menu-toggle" @click="toggleMenu">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </nav>
    </div>
  </header>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMenuOpen = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 1rem 0;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.header.scrolled {
  background: rgba(10, 10, 10, 0.9);
  border-bottom: 1px solid #333;
}

.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo-text {
  font-size: 1.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #f5f5f5 0%, #999 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 2rem;
}

.nav-menu a {
  color: #ccc;
  text-decoration: none;
  font-weight: 500;
  transition: all 0.3s ease;
  position: relative;
}

.nav-menu a:hover {
  color: #f5f5f5;
}

.nav-menu a::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(135deg, #666 0%, #888 100%);
  transition: width 0.3s ease;
}

.nav-menu a:hover::after {
  width: 100%;
}

.menu-toggle {
  display: none;
  flex-direction: column;
  gap: 4px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
}

.menu-toggle span {
  width: 25px;
  height: 2px;
  background: #f5f5f5;
  transition: all 0.3s ease;
}

@media (max-width: 768px) {
  .nav-menu {
    position: fixed;
    top: 70px;
    left: -100%;
    flex-direction: column;
    background: rgba(10, 10, 10, 0.95);
    width: 100%;
    padding: 2rem;
    transition: left 0.3s ease;
    backdrop-filter: blur(10px);
  }

  .nav-menu.active {
    left: 0;
  }

  .menu-toggle {
    display: flex;
  }

  .menu-toggle.active span:nth-child(1) {
    transform: rotate(45deg) translate(5px, 5px);
  }

  .menu-toggle.active span:nth-child(2) {
    opacity: 0;
  }

  .menu-toggle.active span:nth-child(3) {
    transform: rotate(-45deg) translate(7px, -6px);
  }
}

@media (max-width: 992px) {
  .header {
    padding: 0.75rem 0;
  }
  
  .logo-text {
    font-size: 1.375rem;
  }
  
  .nav-menu {
    gap: 1.5rem;
  }
}

@media (max-width: 576px) {
  .header {
    padding: 0.5rem 0;
  }
  
  .logo-text {
    font-size: 1.25rem;
  }
  
  .nav-menu {
    top: 60px;
    padding: 1.5rem;
  }
  
  .nav-menu a {
    font-size: 1.125rem;
    padding: 0.75rem 0;
  }
}

@media (max-width: 480px) {
  .logo-text {
    font-size: 1.125rem;
  }
  
  .menu-toggle {
    padding: 0.25rem;
  }
  
  .menu-toggle span {
    width: 20px;
    height: 1.5px;
  }
}

@media (max-width: 360px) {
  .nav-menu {
    padding: 1rem;
  }
  
  .nav-menu a {
    font-size: 1rem;
  }
}
</style>