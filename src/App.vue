<template>
  <div id="app">
    <NavBar :current-page="currentPage" @navigate="handleNavigate" />
    <component :is="currentComponent" @navigate="handleNavigate" />
    <Footer />
    <Toast v-if="toastMessage" :message="toastMessage" @close="toastMessage = ''" />
  </div>
</template>

<script setup>
import { ref, computed, provide } from 'vue'
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'
import HomePage from './pages/HomePage.vue'
import ProductsPage from './pages/ProductsPage.vue'
import ToolsPage from './pages/ToolsPage.vue'
import ContactPage from './pages/ContactPage.vue'
import Toast from './components/Toast.vue'

const currentPage = ref('home')
const toastMessage = ref('')

const currentComponent = computed(() => {
  const pages = {
    home: HomePage,
    products: ProductsPage,
    tools: ToolsPage,
    contact: ContactPage
  }
  return pages[currentPage.value] || HomePage
})

const handleNavigate = (page) => {
  currentPage.value = page
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const showToast = (message) => {
  toastMessage.value = message
  setTimeout(() => {
    toastMessage.value = ''
  }, 3000)
}

provide('showToast', showToast)
provide('navigate', handleNavigate)
</script>

<style scoped>
#app {
  min-height: 100vh;
}
</style>

