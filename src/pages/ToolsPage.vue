<template>
  <div class="tools-page">
    <section class="tools-section">
      <div class="tools-header">
        <h2 class="section-title">AI工具合集</h2>
        <div class="search-box">
          <input 
            type="text" 
            class="search-input" 
            v-model="searchTerm"
            placeholder="搜索工具名称或描述..."
          >
          <span class="search-icon">🔍</span>
        </div>
      </div>

      <div class="tools-grid">
        <div 
          v-for="tool in currentTools" 
          :key="tool.id"
          class="tool-card"
        >
          <div class="tool-icon" v-if="tool.icon">{{ tool.icon }}</div>
          <h4>{{ tool.name }}</h4>
          <p>{{ tool.desc }}</p>
          <div class="tool-buttons">
            <button 
              v-if="tool.type === 'download'"
              class="btn-download" 
              @click="handleDownload(tool)"
            >
              点击获取
            </button>
            <button 
              v-else
              class="btn-link" 
              @click="handleLink(tool)"
            >
              点击跳转
            </button>
            <button 
              class="btn-tutorial" 
              @click="handleTutorial(tool)"
            >
              使用教程
            </button>
          </div>
        </div>
      </div>

      <div class="pagination" v-if="totalPages > 1">
        <button 
          class="page-btn" 
          @click="changePage(currentPage - 1)"
          :disabled="currentPage === 1"
        >
          上一页
        </button>
        <button 
          v-for="page in visiblePages" 
          :key="page"
          class="page-btn" 
          :class="{ active: page === currentPage }"
          @click="changePage(page)"
          v-if="page !== '...'"
        >
          {{ page }}
        </button>
        <span v-if="visiblePages.includes('...')" style="padding: 10px;">...</span>
        <button 
          class="page-btn" 
          @click="changePage(currentPage + 1)"
          :disabled="currentPage === totalPages"
        >
          下一页
        </button>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { inject } from 'vue'
import { toolsData } from '../data/tools.js'

const showToast = inject('showToast')
const navigate = inject('navigate')

const searchTerm = ref('')
const currentPage = ref(1)
const toolsPerPage = 9

const filteredTools = computed(() => {
  if (!searchTerm.value) {
    return toolsData
  }
  const term = searchTerm.value.toLowerCase()
  return toolsData.filter(tool => 
    tool.name.toLowerCase().includes(term) || 
    tool.desc.toLowerCase().includes(term)
  )
})

const totalPages = computed(() => {
  return Math.ceil(filteredTools.value.length / toolsPerPage)
})

const currentTools = computed(() => {
  const startIndex = (currentPage.value - 1) * toolsPerPage
  const endIndex = startIndex + toolsPerPage
  return filteredTools.value.slice(startIndex, endIndex)
})

const visiblePages = computed(() => {
  const pages = []
  const total = totalPages.value
  
  if (total <= 7) {
    for (let i = 1; i <= total; i++) {
      pages.push(i)
    }
  } else {
    pages.push(1)
    if (currentPage.value > 3) {
      pages.push('...')
    }
    for (let i = Math.max(2, currentPage.value - 1); i <= Math.min(total - 1, currentPage.value + 1); i++) {
      pages.push(i)
    }
    if (currentPage.value < total - 2) {
      pages.push('...')
    }
    pages.push(total)
  }
  
  return pages
})

const changePage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page
    window.scrollTo({ top: 0, behavior: 'smooth' })
  }
}

const handleDownload = (tool) => {
  showToast(`正在下载：${tool.name}`)
  // 实际项目中这里会触发真实的下载
}

const handleLink = (tool) => {
  if (tool.url) {
    window.open(tool.url, '_blank')
  } else {
    showToast(`正在跳转到：${tool.name}`)
  }
}

const handleTutorial = (tool) => {
  // 如果有教程链接，直接打开
  if (tool.tutorialUrl) {
    window.open(tool.tutorialUrl, '_blank')
  } else {
    // 没有教程链接，跳转到联系我们页面
    navigate('contact')
    setTimeout(() => {
      showToast(`请在留言中说明需要"${tool.name}"的使用教程`)
    }, 500)
  }
}
</script>

<style scoped>
.tools-page {
    min-height: calc(100vh - 80px);
    margin-top: 80px;
}

.tools-section {
    padding: 100px 40px;
    background: #F5F5F7;
}

.tools-header {
    max-width: 1200px;
    margin: 0 auto 40px;
}

.section-title {
    text-align: center;
    font-size: 48px;
    font-weight: 700;
    margin-bottom: 40px;
    color: #1D1D1F;
}

.search-box {
    max-width: 600px;
    margin: 0 auto;
    position: relative;
}

.search-input {
    width: 100%;
    padding: 16px 50px 16px 20px;
    border: 2px solid rgba(0, 0, 0, 0.1);
    border-radius: 12px;
    font-size: 16px;
    background: #FFFFFF;
    transition: border-color 0.3s;
}

.search-input:focus {
    outline: none;
    border-color: #1D4ED8;
}

.search-icon {
    position: absolute;
    right: 20px;
    top: 50%;
    transform: translateY(-50%);
    color: #6E6E73;
    font-size: 20px;
    pointer-events: none;
}

.tools-grid {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 24px;
}

.tool-card {
    background: #FFFFFF;
    border: 1px solid rgba(0, 0, 0, 0.05);
    border-radius: 12px;
    padding: 24px;
    transition: transform 0.3s, box-shadow 0.3s;
}

.tool-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
}

.tool-icon {
    width: 60px;
    height: 60px;
    background: linear-gradient(135deg, #1D4ED8 0%, #0066CC 100%);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    margin-bottom: 16px;
}

.tool-card h4 {
    font-size: 20px;
    color: #1D1D1F;
    margin-bottom: 8px;
}

.tool-card p {
    font-size: 14px;
    color: #6E6E73;
    margin-bottom: 16px;
    line-height: 1.6;
}

.tool-buttons {
    display: flex;
    gap: 12px;
}

.btn-download,
.btn-link,
.btn-tutorial {
    flex: 1;
    padding: 10px 20px;
    border: none;
    border-radius: 8px;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
}

.btn-download {
    background: #1D4ED8;
    color: #FFFFFF;
}

.btn-download:hover {
    background: #1E40AF;
}

.btn-link {
    background: #1D4ED8;
    color: #FFFFFF;
}

.btn-link:hover {
    background: #1E40AF;
}

.btn-tutorial {
    background: #1D4ED8;
    color: #FFFFFF;
}

.btn-tutorial:hover {
    background: #1E40AF;
}

.pagination {
    display: flex;
    justify-content: center;
    gap: 12px;
    margin-top: 40px;
    flex-wrap: wrap;
}

.page-btn {
    padding: 10px 16px;
    border: 1px solid rgba(0, 0, 0, 0.1);
    background: #FFFFFF;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s;
}

.page-btn:hover:not(:disabled),
.page-btn.active {
    background: #1D4ED8;
    color: #FFFFFF;
    border-color: #1D4ED8;
}

.page-btn:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}

@media (max-width: 768px) {
    .tools-grid {
        grid-template-columns: 1fr;
    }
}
</style>

