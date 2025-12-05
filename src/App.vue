<template>
  <div id="app">
    <NavBar :current-page="currentPage" @navigate="handleNavigate" />
    <component :is="currentComponent" :key="currentPage" @navigate="handleNavigate" />
    <Footer />
    <Toast v-if="toastMessage" :message="toastMessage" @close="toastMessage = ''" />
  </div>
</template>

<script setup>
import { ref, computed, provide, watch, onMounted } from 'vue'
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'
import HomePage from './pages/HomePage.vue'
import ProductsPage from './pages/ProductsPage.vue'
import ToolsPage from './pages/ToolsPage.vue'
import BlogPage from './pages/BlogPage.vue'
import BlogDetailPage from './pages/BlogDetailPage.vue'
import ContactPage from './pages/ContactPage.vue'
import Toast from './components/Toast.vue'

const currentPage = ref('home')
const toastMessage = ref('')
const pageParams = ref({})

// 页面 SEO 配置 - 优化品牌词"瑞幻智能"位置
const pageSEO = {
  home: {
    title: '瑞幻智能 | RaySo.AI - 全球领先的AI智能解决方案提供商',
    description: '瑞幻智能（RaySo.AI）专注于AI全网营销、AI智能体应用、AI自动化开发与AI视觉检测的创新科技公司。瑞幻智能提供企业级AI解决方案，服务120+企业客户，覆盖12个行业。',
    keywords: '瑞幻智能,AI智能解决方案,AI全网营销,AI智能体应用,AI自动化开发,AI视觉检测,人工智能,机器学习,深度学习,企业AI服务,RaySo.AI'
  },
  products: {
    title: '瑞幻智能 - 产品与服务 | AI智能解决方案',
    description: '瑞幻智能提供AI全网营销、AI智能体应用、AI自动化开发、AI视觉检测等企业级AI解决方案。瑞幻智能助力企业数字化转型，提升业务效率。',
    keywords: '瑞幻智能,AI产品,AI服务,AI解决方案,AI全网营销,AI智能体,AI自动化开发,AI视觉检测,RaySo.AI'
  },
  tools: {
    title: '瑞幻智能 - AI工具合集 | 免费AI工具下载',
    description: '瑞幻智能精选AI工具合集，包括AI提示词管理、AI视频广告生成、AI软著材料生成等实用工具。瑞幻智能助力AI应用开发。',
    keywords: '瑞幻智能,AI工具,AI应用,AI开发工具,AI提示词,AI视频生成,AI工具下载,RaySo.AI'
  },
  blog: {
    title: '瑞幻智能 - 博客与教程 | AI技术文章',
    description: '瑞幻智能博客提供AI技术教程、科普文章、行业动态、产品更新等专业内容。瑞幻智能帮助开发者和企业了解AI技术最新发展。',
    keywords: '瑞幻智能,AI教程,AI技术,AI博客,AI科普,AI行业动态,AI开发教程,RaySo.AI'
  },
  'blog-detail': {
    title: '',
    description: ''
  },
  contact: {
    title: '瑞幻智能 - 联系我们 | AI咨询服务',
    description: '联系瑞幻智能，获取AI智能解决方案咨询服务。瑞幻智能邮箱：zzrayhuan@163.com，微信：rayhuan520。瑞幻智能专业团队为您服务。',
    keywords: '瑞幻智能,联系我们,AI咨询,AI服务咨询,瑞幻智能联系方式,RaySo.AI'
  }
}

// 更新页面 SEO
const updatePageSEO = (page) => {
  const seo = pageSEO[page] || pageSEO.home
  
  // 更新 title
  if (seo.title) {
    document.title = seo.title
  }
  
  // 更新 meta description
  let metaDescription = document.querySelector('meta[name="description"]')
  if (metaDescription) {
    metaDescription.setAttribute('content', seo.description)
  } else {
    metaDescription = document.createElement('meta')
    metaDescription.name = 'description'
    metaDescription.content = seo.description
    document.head.appendChild(metaDescription)
  }
  
  // 更新 meta keywords
  let metaKeywords = document.querySelector('meta[name="keywords"]')
  if (seo.keywords) {
    if (metaKeywords) {
      metaKeywords.setAttribute('content', seo.keywords)
    } else {
      metaKeywords = document.createElement('meta')
      metaKeywords.name = 'keywords'
      metaKeywords.content = seo.keywords
      document.head.appendChild(metaKeywords)
    }
  }
  
  // 更新 Open Graph
  const updateOG = (property, content) => {
    let ogTag = document.querySelector(`meta[property="${property}"]`)
    if (ogTag) {
      ogTag.setAttribute('content', content)
    } else {
      ogTag = document.createElement('meta')
      ogTag.setAttribute('property', property)
      ogTag.setAttribute('content', content)
      document.head.appendChild(ogTag)
    }
  }
  
  if (seo.title) {
    updateOG('og:title', seo.title)
  }
  if (seo.description) {
    updateOG('og:description', seo.description)
  }
  updateOG('og:url', `https://rayso.ai/${page === 'home' ? '' : page}`)
}

const currentComponent = computed(() => {
  const pages = {
    home: HomePage,
    products: ProductsPage,
    tools: ToolsPage,
    blog: BlogPage,
    'blog-detail': BlogDetailPage,
    contact: ContactPage
  }
  return pages[currentPage.value] || HomePage
})

const handleNavigate = (page, params = {}) => {
  currentPage.value = page
  pageParams.value = params
  window.scrollTo({ top: 0, behavior: 'smooth' })
  
  // 如果是博客详情页，设置 blogId
  if (page === 'blog-detail' && params.blogId) {
    window.blogDetailId = params.blogId
  }
  
  // 更新 SEO
  updatePageSEO(page)
}

// 监听页面变化，更新 SEO
watch(currentPage, (newPage) => {
  updatePageSEO(newPage)
})

// 初始化 SEO
onMounted(() => {
  updatePageSEO(currentPage.value)
})

provide('pageParams', pageParams)

const showToast = (message) => {
  toastMessage.value = message
  setTimeout(() => {
    toastMessage.value = ''
  }, 3000)
}

provide('showToast', showToast)
provide('navigate', handleNavigate)
provide('updateSEO', updatePageSEO)
</script>

<style scoped>
#app {
  min-height: 100vh;
}
</style>

