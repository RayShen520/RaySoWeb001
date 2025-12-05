<template>
  <div class="blog-page">
    <main>
    <section class="blog-section">
      <h1 class="section-title">瑞幻智能 - 博客与教程</h1>
      
      <!-- 搜索和筛选 -->
      <div class="blog-filters">
        <div class="search-box">
          <input 
            type="text" 
            class="search-input" 
            v-model="searchTerm"
            placeholder="搜索文章标题或内容..."
          >
          <span class="search-icon">🔍</span>
        </div>
        <div class="category-filters">
          <button 
            v-for="category in categories" 
            :key="category"
            class="filter-btn" 
            :class="{ active: currentCategory === category }"
            @click="filterByCategory(category)"
          >
            {{ category }}
          </button>
        </div>
      </div>

      <!-- 文章列表 -->
      <div class="blog-grid" v-if="filteredBlogs.length > 0">
        <div 
          v-for="blog in paginatedBlogs" 
          :key="blog.id"
          class="blog-card"
          @click="showDetail(blog.id)"
        >
          <div class="blog-card-header">
            <span class="blog-category">{{ blog.category }}</span>
            <h3 class="blog-card-title">{{ blog.title }}</h3>
            <p class="blog-card-excerpt">{{ blog.excerpt }}</p>
          </div>
          <div class="blog-card-footer">
            <span class="blog-card-date">{{ blog.date }}</span>
            <div class="blog-card-tags">
              <span 
                v-for="tag in blog.tags.slice(0, 3)" 
                :key="tag"
                class="blog-tag"
              >
                {{ tag }}
              </span>
            </div>
          </div>
        </div>
      </div>

      <div v-else class="empty-state">
        <p>暂无文章</p>
      </div>

      <!-- 分页 -->
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
          :class="{ active: currentPage === page }"
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
    </main>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { blogArticles } from '../data/blog.js'
import { inject } from 'vue'

const navigate = inject('navigate')

const searchTerm = ref('')
const currentCategory = ref('全部')
const currentPage = ref(1)
const blogsPerPage = 9

const categories = ['全部', '技术教程', '科普文章', '行业动态', '产品更新']

const filteredBlogs = computed(() => {
  return blogArticles.filter(blog => {
    // 分类筛选
    const categoryMatch = currentCategory.value === '全部' || blog.category === currentCategory.value
    
    // 搜索筛选
    const searchMatch = !searchTerm.value || 
      blog.title.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      blog.excerpt.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      blog.content.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      blog.tags.some(tag => tag.toLowerCase().includes(searchTerm.value.toLowerCase()))
    
    return categoryMatch && searchMatch
  })
})

const totalPages = computed(() => {
  return Math.ceil(filteredBlogs.value.length / blogsPerPage)
})

const paginatedBlogs = computed(() => {
  const startIndex = (currentPage.value - 1) * blogsPerPage
  const endIndex = startIndex + blogsPerPage
  return filteredBlogs.value.slice(startIndex, endIndex)
})

const visiblePages = computed(() => {
  const pages = []
  const total = totalPages.value
  const current = currentPage.value
  
  if (total <= 7) {
    for (let i = 1; i <= total; i++) {
      pages.push(i)
    }
  } else {
    pages.push(1)
    if (current > 3) pages.push('...')
    
    for (let i = Math.max(2, current - 1); i <= Math.min(total - 1, current + 1); i++) {
      pages.push(i)
    }
    
    if (current < total - 2) pages.push('...')
    pages.push(total)
  }
  
  return pages
})

const filterByCategory = (category) => {
  currentCategory.value = category
  currentPage.value = 1
}

const changePage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page
    window.scrollTo({ top: 0, behavior: 'smooth' })
  }
}

const showDetail = (blogId) => {
  // 设置全局变量，供 BlogDetailPage 使用
  window.blogDetailId = blogId
  navigate('blog-detail')
}

onMounted(() => {
  // 添加面包屑导航结构化数据
  const breadcrumbSchema = {
    "@context": "https://schema.org",
    "@type": "BreadcrumbList",
    "itemListElement": [
      {
        "@type": "ListItem",
        "position": 1,
        "name": "首页",
        "item": "https://rayso.ai/"
      },
      {
        "@type": "ListItem",
        "position": 2,
        "name": "博客/教程",
        "item": "https://rayso.ai/blog"
      }
    ]
  }
  
  let existingSchema = document.getElementById('blog-breadcrumb-schema')
  if (!existingSchema) {
    const schemaScript = document.createElement('script')
    schemaScript.type = 'application/ld+json'
    schemaScript.id = 'blog-breadcrumb-schema'
    schemaScript.textContent = JSON.stringify(breadcrumbSchema)
    document.head.appendChild(schemaScript)
  }
})
</script>

<style scoped>
.blog-page {
  min-height: calc(100vh - 80px);
  margin-top: 80px;
}

.blog-section {
  padding: 100px 40px;
  background: #FFFFFF;
}

.section-title {
  text-align: center;
  font-size: 48px;
  font-weight: 700;
  margin-bottom: 60px;
  color: #1D1D1F;
}

.blog-filters {
  max-width: 1200px;
  margin: 0 auto 40px;
}

.blog-filters .search-box {
  max-width: 600px;
  margin: 0 auto 30px;
  position: relative;
}

.blog-filters .search-input {
  width: 100%;
  padding: 16px 50px 16px 20px;
  border: 2px solid rgba(0, 0, 0, 0.1);
  border-radius: 12px;
  font-size: 16px;
  background: #FFFFFF;
  transition: border-color 0.3s;
}

.blog-filters .search-input:focus {
  outline: none;
  border-color: #1D4ED8;
}

.blog-filters .search-icon {
  position: absolute;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  color: #6E6E73;
  font-size: 20px;
  pointer-events: none;
}

.category-filters {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 12px;
}

.filter-btn {
  padding: 8px 20px;
  border: 2px solid rgba(0, 0, 0, 0.1);
  background: #FFFFFF;
  border-radius: 20px;
  font-size: 14px;
  font-weight: 500;
  color: #1D1D1F;
  cursor: pointer;
  transition: all 0.3s;
}

.filter-btn:hover {
  border-color: #1D4ED8;
  color: #1D4ED8;
}

.filter-btn.active {
  background: #1D4ED8;
  color: #FFFFFF;
  border-color: #1D4ED8;
}

.blog-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 30px;
}

.blog-card {
  background: #FFFFFF;
  border: 1px solid rgba(0, 0, 0, 0.05);
  border-radius: 16px;
  overflow: hidden;
  transition: transform 0.3s, box-shadow 0.3s;
  cursor: pointer;
}

.blog-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.blog-card-header {
  padding: 24px 24px 16px;
}

.blog-category {
  display: inline-block;
  background: #1D4ED8;
  color: #FFFFFF;
  padding: 4px 12px;
  border-radius: 12px;
  font-size: 12px;
  font-weight: 600;
  margin-bottom: 12px;
}

.blog-card-title {
  font-size: 20px;
  font-weight: 600;
  color: #1D1D1F;
  margin-bottom: 12px;
  line-height: 1.4;
}

.blog-card-excerpt {
  font-size: 14px;
  color: #6E6E73;
  line-height: 1.6;
  margin-bottom: 16px;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.blog-card-footer {
  padding: 16px 24px;
  border-top: 1px solid rgba(0, 0, 0, 0.05);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.blog-card-date {
  font-size: 12px;
  color: #6E6E73;
}

.blog-card-tags {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
}

.blog-tag {
  font-size: 11px;
  color: #1D4ED8;
  background: rgba(29, 78, 216, 0.1);
  padding: 2px 8px;
  border-radius: 10px;
}

.empty-state {
  text-align: center;
  padding: 60px;
  color: #6E6E73;
}

.pagination {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-top: 40px;
}

.page-btn {
  padding: 10px 16px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  background: #FFFFFF;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s;
  font-size: 14px;
}

.page-btn:hover:not(:disabled) {
  background: #1D4ED8;
  color: #FFFFFF;
  border-color: #1D4ED8;
}

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
  .blog-section {
    padding: 40px 20px;
  }

  .section-title {
    font-size: 32px;
    margin-bottom: 30px;
  }

  .blog-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .blog-card-header {
    padding: 20px;
  }

  .blog-card-title {
    font-size: 18px;
  }
}
</style>

