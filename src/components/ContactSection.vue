<template>
  <section id="contact" class="section contact">
    <div class="container">
      <div class="section-header fade-in">
        <h2 class="section-title">Get In Touch</h2>
        <p class="section-subtitle">Let's work together to bring your ideas to life</p>
      </div>
      
      <div class="contact-content">
        <div class="contact-info fade-in">
          <div class="contact-item">
            <div class="contact-icon">📧</div>
            <div class="contact-details">
              <h3>Email</h3>
              <p>samudofia91@gmail.com</p>
            </div>
          </div>
          
          <div class="contact-item">
            <div class="contact-icon">📱</div>
            <div class="contact-details">
              <h3>Phone</h3>
              <p>+234 7018030002</p>
            </div>
          </div>
          
          <div class="contact-item">
            <div class="contact-icon">📍</div>
            <div class="contact-details">
              <h3>Location</h3>
              <p>Lagos, Nigeria</p>
            </div>
          </div>
          
          <div class="social-links">
            <a href="#" class="social-link">LinkedIn</a>
            <a href="#" class="social-link">GitHub</a>
            <a href="#" class="social-link">Twitter</a>
          </div>
        </div>
        
        <form class="contact-form fade-in" @submit.prevent="handleSubmit">
          <div class="form-group">
            <label for="name">Name</label>
            <input
              type="text"
              id="name"
              v-model="form.name"
              :class="{ 'error': errors.name }"
              required
            />
            <span v-if="errors.name" class="error-message">{{ errors.name }}</span>
          </div>
          
          <div class="form-group">
            <label for="email">Email</label>
            <input
              type="email"
              id="email"
              v-model="form.email"
              :class="{ 'error': errors.email }"
              required
            />
            <span v-if="errors.email" class="error-message">{{ errors.email }}</span>
          </div>
          
          <div class="form-group">
            <label for="subject">Subject</label>
            <input
              type="text"
              id="subject"
              v-model="form.subject"
              :class="{ 'error': errors.subject }"
              required
            />
            <span v-if="errors.subject" class="error-message">{{ errors.subject }}</span>
          </div>
          
          <div class="form-group">
            <label for="message">Message</label>
            <textarea
              id="message"
              v-model="form.message"
              :class="{ 'error': errors.message }"
              rows="5"
              required
            ></textarea>
            <span v-if="errors.message" class="error-message">{{ errors.message }}</span>
          </div>
          
          <button
            type="submit"
            class="btn btn-primary submit-btn"
            :disabled="isSubmitting"
          >
            {{ isSubmitting ? 'Sending...' : 'Send Message' }}
          </button>
          
          <div v-if="submitMessage" class="submit-message" :class="submitStatus">
            {{ submitMessage }}
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted } from 'vue'

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const errors = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const isSubmitting = ref(false)
const submitMessage = ref('')
const submitStatus = ref('')

const validateForm = () => {
  Object.keys(errors).forEach(key => errors[key as keyof typeof errors] = '')
  
  let isValid = true
  
  if (!form.name.trim()) {
    errors.name = 'Name is required'
    isValid = false
  }
  
  if (!form.email.trim()) {
    errors.email = 'Email is required'
    isValid = false
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
    errors.email = 'Please enter a valid email'
    isValid = false
  }
  
  if (!form.subject.trim()) {
    errors.subject = 'Subject is required'
    isValid = false
  }
  
  if (!form.message.trim()) {
    errors.message = 'Message is required'
    isValid = false
  }
  
  return isValid
}

const handleSubmit = async () => {
  if (!validateForm()) return
  
  isSubmitting.value = true
  submitMessage.value = ''
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    submitMessage.value = 'Message sent successfully! I\'ll get back to you soon.'
    submitStatus.value = 'success'
    
    // Reset form
    Object.keys(form).forEach(key => form[key as keyof typeof form] = '')
  } catch (error) {
    submitMessage.value = 'Failed to send message. Please try again.'
    submitStatus.value = 'error'
  } finally {
    isSubmitting.value = false
    setTimeout(() => {
      submitMessage.value = ''
    }, 5000)
  }
}

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
.contact {
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

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 4rem;
  align-items: start;
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.5rem;
  background: rgba(26, 26, 26, 0.5);
  border-radius: 12px;
  border: 1px solid #333;
  transition: all 0.3s ease;
}

.contact-item:hover {
  background: rgba(26, 26, 26, 0.8);
  border-color: #444;
  transform: translateY(-2px);
}

.contact-icon {
  font-size: 1.5rem;
  width: 3rem;
  height: 3rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(102, 102, 102, 0.2);
  border-radius: 50%;
  border: 1px solid #444;
}

.contact-details h3 {
  color: #f5f5f5;
  font-size: 1.125rem;
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.contact-details p {
  color: #bbb;
}

.social-links {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
}

.social-link {
  padding: 0.75rem 1.5rem;
  background: rgba(102, 102, 102, 0.2);
  color: #ccc;
  text-decoration: none;
  border-radius: 25px;
  border: 1px solid #444;
  transition: all 0.3s ease;
  font-weight: 500;
}

.social-link:hover {
  background: rgba(102, 102, 102, 0.3);
  color: #f5f5f5;
  transform: translateY(-2px);
}

.contact-form {
  background: rgba(26, 26, 26, 0.5);
  padding: 2rem;
  border-radius: 12px;
  border: 1px solid #333;
  backdrop-filter: blur(10px);
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  color: #f5f5f5;
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  background: rgba(10, 10, 10, 0.8);
  border: 1px solid #444;
  border-radius: 8px;
  color: #f5f5f5;
  font-size: 1rem;
  transition: all 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #666;
  background: rgba(10, 10, 10, 0.9);
}

.form-group input.error,
.form-group textarea.error {
  border-color: #e74c3c;
}

.error-message {
  color: #e74c3c;
  font-size: 0.875rem;
  margin-top: 0.25rem;
  display: block;
}

.submit-btn {
  width: 100%;
  justify-content: center;
  padding: 1rem;
  font-size: 1.125rem;
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.submit-message {
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 8px;
  text-align: center;
  font-weight: 500;
}

.submit-message.success {
  background: rgba(46, 204, 113, 0.2);
  color: #2ecc71;
  border: 1px solid #2ecc71;
}

.submit-message.error {
  background: rgba(231, 76, 60, 0.2);
  color: #e74c3c;
  border: 1px solid #e74c3c;
}

@media (max-width: 968px) {
  .contact-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}

@media (max-width: 768px) {
  .social-links {
    flex-wrap: wrap;
  }
  
  .contact-form {
    padding: 1.5rem;
  }
}

@media (max-width: 1200px) {
  .contact-content {
    gap: 3.5rem;
  }
}

@media (max-width: 992px) {
  .section-title {
    font-size: clamp(1.75rem, 3.5vw, 2.5rem);
  }
  
  .section-subtitle {
    font-size: 1rem;
  }
  
  .contact-item {
    padding: 1.25rem;
  }
  
  .contact-details h3 {
    font-size: 1rem;
  }
  
  .contact-details p {
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
  
  .contact-content {
    gap: 2.5rem;
  }
  
  .contact-info {
    gap: 1.5rem;
  }
  
  .contact-item {
    padding: 1rem;
    flex-direction: column;
    text-align: center;
    gap: 0.75rem;
  }
  
  .contact-icon {
    font-size: 1.25rem;
    width: 2.5rem;
    height: 2.5rem;
  }
  
  .contact-details h3 {
    font-size: 0.95rem;
    margin-bottom: 0.125rem;
  }
  
  .contact-details p {
    font-size: 0.9rem;
  }
  
  .social-links {
    justify-content: center;
    gap: 0.75rem;
  }
  
  .social-link {
    padding: 0.625rem 1.25rem;
    font-size: 0.875rem;
  }
  
  .contact-form {
    padding: 1.25rem;
  }
  
  .form-group {
    margin-bottom: 1.25rem;
  }
  
  .form-group label {
    font-size: 0.95rem;
    margin-bottom: 0.375rem;
  }
  
  .form-group input,
  .form-group textarea {
    padding: 0.625rem 0.875rem;
    font-size: 0.95rem;
  }
  
  .submit-btn {
    padding: 0.875rem;
    font-size: 1rem;
  }
}

@media (max-width: 480px) {
  .section-header {
    margin-bottom: 2.5rem;
  }
  
  .contact-content {
    gap: 2rem;
  }
  
  .contact-info {
    gap: 1.25rem;
  }
  
  .contact-item {
    padding: 0.875rem;
    border-radius: 10px;
  }
  
  .contact-icon {
    font-size: 1.125rem;
    width: 2.25rem;
    height: 2.25rem;
  }
  
  .contact-details h3 {
    font-size: 0.9rem;
  }
  
  .contact-details p {
    font-size: 0.85rem;
  }
  
  .social-link {
    padding: 0.5rem 1rem;
    font-size: 0.8rem;
  }
  
  .contact-form {
    padding: 1rem;
    border-radius: 10px;
  }
  
  .form-group input,
  .form-group textarea {
    padding: 0.5rem 0.75rem;
    font-size: 0.9rem;
  }
  
  .submit-btn {
    padding: 0.75rem;
    font-size: 0.95rem;
  }
  
  .submit-message {
    padding: 0.875rem;
    font-size: 0.9rem;
  }
}

@media (max-width: 360px) {
  .contact-item {
    padding: 0.75rem;
  }
  
  .contact-icon {
    width: 2rem;
    height: 2rem;
    font-size: 1rem;
  }
  
  .contact-details h3 {
    font-size: 0.85rem;
  }
  
  .contact-details p {
    font-size: 0.8rem;
  }
  
  .social-links {
    gap: 0.5rem;
  }
  
  .social-link {
    padding: 0.45rem 0.875rem;
    font-size: 0.75rem;
  }
  
  .contact-form {
    padding: 0.875rem;
  }
  
  .form-group {
    margin-bottom: 1rem;
  }
  
  .form-group label {
    font-size: 0.9rem;
  }
  
  .form-group input,
  .form-group textarea {
    font-size: 0.85rem;
  }
  
  .submit-btn {
    font-size: 0.9rem;
  }
}
</style>