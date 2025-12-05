<template>
  <nav class="navbar" :class="{ scrolled: isScrolled }" id="navbar">
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
    <div class="menu-toggle" :class="{ active: isMenuOpen }" @click="toggleMenu">
      <span></span>
      <span></span>
      <span></span>
    </div>
  </nav>
  
  <!-- 移动端菜单 -->
  <div class="mobile-menu" :class="{ active: isMenuOpen }">
    <div class="mobile-menu-links">
      <a 
        v-for="link in navLinks" 
        :key="link.id"
        href="#" 
        :class="{ active: currentPage === link.id }"
        @click.prevent="navigateAndClose(link.id)"
      >
        {{ link.label }}
      </a>
    </div>
  </div>
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
const isMenuOpen = ref(false)
const navLinks = [
  { id: 'home', label: '首页' },
  { id: 'products', label: '产品服务' },
  { id: 'tools', label: 'AI工具合集' },
  { id: 'blog', label: '博客/教程' },
  { id: 'contact', label: '联系我们' }
]

const navigate = (page) => {
  emit('navigate', page)
}

const navigateAndClose = (page) => {
  navigate(page)
  isMenuOpen.value = false
}

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const goHome = () => {
  navigate('home')
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

// 点击外部关闭菜单
const handleClickOutside = (event) => {
  const navbar = document.getElementById('navbar')
  const mobileMenu = document.querySelector('.mobile-menu')
  if (navbar && mobileMenu && !navbar.contains(event.target) && isMenuOpen.value) {
    isMenuOpen.value = false
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  document.addEventListener('click', handleClickOutside)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  document.removeEventListener('click', handleClickOutside)
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

/* 汉堡菜单按钮 */
.menu-toggle {
    display: none;
    flex-direction: column;
    gap: 5px;
    cursor: pointer;
    padding: 5px;
    z-index: 1001;
}

.menu-toggle span {
    width: 25px;
    height: 3px;
    background: #1D1D1F;
    border-radius: 2px;
    transition: all 0.3s;
}

.menu-toggle.active span:nth-child(1) {
    transform: rotate(45deg) translate(8px, 8px);
}

.menu-toggle.active span:nth-child(2) {
    opacity: 0;
}

.menu-toggle.active span:nth-child(3) {
    transform: rotate(-45deg) translate(7px, -7px);
}

/* 移动端菜单 */
.mobile-menu {
    display: none;
    position: fixed;
    top: 80px;
    left: 0;
    width: 100%;
    background: rgba(255, 255, 255, 0.98);
    backdrop-filter: blur(10px);
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    z-index: 999;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease-out;
}

.mobile-menu.active {
    max-height: 500px;
}

.mobile-menu-links {
    display: flex;
    flex-direction: column;
    padding: 20px;
}

.mobile-menu-links a {
    color: #1D1D1F;
    text-decoration: none;
    font-size: 16px;
    padding: 12px 0;
    border-bottom: 1px solid rgba(0, 0, 0, 0.05);
    transition: color 0.3s;
}

.mobile-menu-links a:last-child {
    border-bottom: none;
}

.mobile-menu-links a:hover,
.mobile-menu-links a.active {
    color: #1D4ED8;
}

@media (max-width: 768px) {
    /* 导航栏移动端优化 */
    .navbar {
        padding: 12px 20px;
    }

    .logo {
        font-size: 18px;
    }

    /* 隐藏桌面端导航链接 */
    .nav-links {
        display: none;
    }

    /* 显示汉堡菜单按钮 */
    .menu-toggle {
        display: flex;
    }

    /* 显示移动端菜单 */
    .mobile-menu {
        display: block;
    }
}
</style>

