<template>
  <nav class="navbar" :class="{ scrolled: isScrolled }">
    <div class="logo" @click="goHome">瑞幻智能 | RaySo.AI</div>
    <div class="nav-links">
      <a 
        v-for="link in navLinks" 
        :key="link.id"
        href="#" 
        :class="{ active: currentPage === link.id }"
        @click.prevent="navigate(link.id)"
      >
        {{ link.label }}
      </a>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  currentPage: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['navigate'])

const isScrolled = ref(false)
const navLinks = [
  { id: 'home', label: '首页' },
  { id: 'products', label: '产品服务' },
  { id: 'tools', label: 'AI工具合集' },
  { id: 'contact', label: '联系我们' }
]

const navigate = (page) => {
  emit('navigate', page)
}

const goHome = () => {
  navigate('home')
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.navbar {
    position: fixed;
    top: 0;
    width: 100%;
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(10px);
    padding: 20px 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    z-index: 1000;
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    transition: all 0.3s;
}

.navbar.scrolled {
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.logo {
    font-size: 24px;
    font-weight: 600;
    color: #1D4ED8;
    cursor: pointer;
    transition: opacity 0.3s;
}

.logo:hover {
    opacity: 0.8;
}

.nav-links {
    display: flex;
    gap: 40px;
    align-items: center;
}

.nav-links a {
    color: #1D1D1F;
    text-decoration: none;
    font-size: 16px;
    transition: color 0.3s;
    position: relative;
}

.nav-links a:hover,
.nav-links a.active {
    color: #1D4ED8;
}

.nav-links a.active::after {
    content: '';
    position: absolute;
    bottom: -5px;
    left: 0;
    width: 100%;
    height: 2px;
    background: #1D4ED8;
}

@media (max-width: 768px) {
    .nav-links {
        gap: 20px;
        font-size: 14px;
    }
    
    .navbar {
        padding: 15px 20px;
    }
}
</style>

