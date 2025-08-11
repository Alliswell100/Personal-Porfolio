<template>
  <section id="home" class="hero">
    <div class="hero-bg">
      <div class="floating-shapes">
        <div class="shape shape-1"></div>
        <div class="shape shape-2"></div>
        <div class="shape shape-3"></div>
      </div>
    </div>
    <div class="container">
      <div class="hero-content">
        <img class="heroImage" src="../assets/images/kelvin.png" alt="samuel image">
        <div class="hero-text">
          <h1 class="hero-title">
            <span class="greeting">Hi, I'm</span>
            <span class="name">{{ name }}</span>
          </h1>
          <div class="hero-subtitle">
            <span class="typewriter">{{ displayText }}</span>
            <span class="cursor" :class="{ 'blink': showCursor }">|</span>
          </div>
          <p class="hero-description fade-in">
           I'm a frontend developer who believes that great code is just as much about creative thinking as it is about 
           technical skill. I excel at translating design concepts into seamless, interactive web interfaces, always 
           looking for unique ways to enhance the user experience. I enjoy the process of 
           deconstructing a challenge and building a solution that is not only effective but also delightful to use.
          </p>
          <div class="hero-buttons fade-in">
            <a href="#projects" class="btn btn-primary">View My Work</a>
            <a href="#contact" class="btn">Get In Touch</a>
          </div>
        </div>
      </div>
    </div>
    <div class="scroll-indicator">
      <div class="scroll-arrow"></div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const name = ref('Samuel Godwin')
const texts = ['Frontend Developer', 'Creative Thinker', 'Problem Solver']
const displayText = ref('')
const currentTextIndex = ref(0)
const currentCharIndex = ref(0)
const showCursor = ref(true)
const isDeleting = ref(false)

const typeWriter = () => {
  const currentText = texts[currentTextIndex.value]
  
  if (!isDeleting.value) {
    displayText.value = currentText.substring(0, currentCharIndex.value + 1)
    currentCharIndex.value++
    
    if (currentCharIndex.value === currentText.length) {
      setTimeout(() => isDeleting.value = true,    5000)
    }
  } else {
    displayText.value = currentText.substring(0, currentCharIndex.value - 1)
    currentCharIndex.value--
    
    if (currentCharIndex.value === 0) {
      isDeleting.value = false
      currentTextIndex.value = (currentTextIndex.value + 1) % texts.length
    }
  }
  
  setTimeout(typeWriter, isDeleting.value ? 50 : 100)
}

onMounted(() => {
  setTimeout(typeWriter, 8000)
  
  // Cursor blinking
  setInterval(() => {
    showCursor.value = !showCursor.value
  }, 530)
  
  // Scroll animations
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
      }
    })
  })
  
  document.querySelectorAll('.fade-in').forEach((el) => {
    observer.observe(el)
  })
})
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
  background: radial-gradient(ellipse at center, #1a1a1a 0%, #0a0a0a 100%);
}

.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.heroImage{
  position:relative; 
  width:30%;
  height:20%;
  border-radius: 50%;
} 

.floating-shapes {
  position: absolute;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(102, 102, 102, 0.1) 0%, rgba(136, 136, 136, 0.05) 100%);
  animation: float 6s ease-in-out infinite;
}

.shape-1 {
  width: 200px;
  height: 200px;
  top: 20%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 150px;
  height: 150px;
  top: 60%;
  right: 10%;
  animation-delay: 2s;
}

.shape-3 {
  width: 100px;
  height: 100px;
  top: 40%;
  left: 60%;
  animation-delay: 4s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(180deg); }
}

.hero-content {
  position: relative;
  z-index: 2;
  text-align: center;
}

.hero-title {
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 700;
  margin-bottom: 1rem;
  line-height: 1.2;
}

.greeting {
  display: block;
  font-size: 0.6em;
  color: #999;
  font-weight: 400;
  margin-bottom: 0.5rem;
}

.name {
  display: block;
  background: linear-gradient(135deg, #f5f5f5 0%, #999 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: clamp(1.25rem, 3vw, 2rem);
  margin-bottom: 2rem;
  height: 3rem;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 0.25rem;
}

.typewriter {
  color: #ccc;
  font-weight: 500;
}

.cursor {
  color: #666;
  font-weight: 300;
  transition: opacity 0.1s;
}

.cursor.blink {
  opacity: 0;
}

.hero-description {
  font-size: 1.125rem;
  color: #bbb;
  max-width: 600px;
  margin: 0 auto 2.5rem;
  line-height: 1.8;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
}

.scroll-arrow {
  width: 24px;
  height: 24px;
  border: 2px solid #666;
  border-top: none;
  border-right: none;
  transform: rotate(-45deg);
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% { transform: translateY(0) rotate(-45deg); }
  40% { transform: translateY(-10px) rotate(-45deg); }
  60% { transform: translateY(-5px) rotate(-45deg); }
}

@media (max-width: 768px) {
  .hero-buttons {
    flex-direction: column;
    align-items: center;
  }
  
  .btn {
    width: 200px;
    justify-content: center;
  }
}

@media (max-width: 992px) {
  .hero-title {
    font-size: clamp(2rem, 4.5vw, 3.5rem);
  }
  
  .hero-subtitle {
    font-size: clamp(1.125rem, 2.5vw, 1.75rem);
    height: 2.5rem;
  }
  
  .hero-description {
    font-size: 1rem;
    margin-bottom: 2rem;
  }
  
  .shape-1 {
    width: 150px;
    height: 150px;
  }
  
  .shape-2 {
    width: 120px;
    height: 120px;
  }
  
  .shape-3 {
    width: 80px;
    height: 80px;
  }
}

@media (max-width: 576px) {
  .hero {
    min-height: 90vh;
    padding: 2rem 0;
  }
  
  .hero-title {
    font-size: clamp(1.75rem, 6vw, 2.5rem);
    margin-bottom: 0.75rem;
  }
  
  .greeting {
    font-size: 0.7em;
    margin-bottom: 0.25rem;
  }
  
  .hero-subtitle {
    font-size: clamp(1rem, 4vw, 1.5rem);
    height: 2rem;
    margin-bottom: 1.5rem;
  }
  
  .hero-description {
    font-size: 0.95rem;
    margin-bottom: 1.75rem;
    line-height: 1.6;
  }
  
  .hero-buttons {
    gap: 0.75rem;
  }
  
  .btn {
    width: 180px;
  }
  
  .scroll-indicator {
    bottom: 1rem;
  }
  
  .scroll-arrow {
    width: 20px;
    height: 20px;
  }
}

@media (max-width: 480px) {
  .hero {
    min-height: 85vh;
  }
  
  .hero-title {
    font-size: clamp(1.5rem, 7vw, 2.25rem);
  }
  
  .hero-subtitle {
    font-size: clamp(0.9rem, 5vw, 1.25rem);
    height: 1.75rem;
  }
  
  .hero-description {
    font-size: 0.9rem;
    margin-bottom: 1.5rem;
  }
  
  .btn {
    width: 160px;
    padding: 0.6rem 1rem;
  }
  
  .shape-1, .shape-2, .shape-3 {
    display: none;
  }
}

@media (max-width: 360px) {
  .hero {
    min-height: 80vh;
  }
  
  .hero-content {
    padding: 1rem 0;
  }
  
  .hero-title {
    font-size: clamp(1.375rem, 8vw, 2rem);
  }
  
  .hero-subtitle {
    font-size: clamp(0.85rem, 6vw, 1.125rem);
    height: 1.5rem;
  }
  
  .hero-description {
    font-size: 0.85rem;
  }
  
  .btn {
    width: 140px;
    font-size: 0.8rem;
  }
}
</style>