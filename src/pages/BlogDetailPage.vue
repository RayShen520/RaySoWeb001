<template>
  <div class="blog-detail-page">
    <main>
    <section class="blog-detail-section">
      <div class="blog-detail-container">
        <button class="back-btn" @click="goBack" aria-label="返回博客列表">← 返回列表</button>
        <article class="blog-article" v-if="blog" itemscope itemtype="https://schema.org/BlogPosting">
          <div class="article-header">
            <span class="article-category">{{ blog.category }}</span>
            <h1 class="article-title">{{ blog.title }}</h1>
            <div class="article-meta">
              <span>📅 {{ blog.date }}</span>
              <span>✍️ {{ blog.author }}</span>
            </div>
            <div class="article-tags">
              <span 
                v-for="tag in blog.tags" 
                :key="tag"
                class="article-tag"
              >
                {{ tag }}
              </span>
            </div>
          </div>
          <div 
            class="article-content" 
            v-html="renderedContent"
          ></div>
        </article>
        <div v-else class="loading-state">
          <p>加载中...</p>
        </div>
      </div>
    </section>
    </main>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, nextTick, watch } from 'vue'
import { blogArticles } from '../data/blog.js'
import { inject } from 'vue'

const navigate = inject('navigate')

const blogId = ref(null)
const blog = ref(null)

// 更新博客详情页 SEO
const updateBlogSEO = (blogData) => {
  if (!blogData) return
  
  // 更新 title - 确保"瑞幻智能"在最前面
  document.title = '瑞幻智能 - ' + blogData.title + ' | RaySo.AI'
  
  // 更新 meta description
  let metaDescription = document.querySelector('meta[name="description"]')
  if (metaDescription) {
    metaDescription.setAttribute('content', blogData.excerpt)
  } else {
    metaDescription = document.createElement('meta')
    metaDescription.name = 'description'
    metaDescription.content = blogData.excerpt
    document.head.appendChild(metaDescription)
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
  
  updateOG('og:title', blogData.title)
  updateOG('og:description', blogData.excerpt)
  updateOG('og:url', `https://rayso.ai/blog/${blogData.id}`)
  updateOG('og:type', 'article')
  
  // 添加 Article 结构化数据
  const existingArticleSchema = document.getElementById('blog-article-schema')
  if (existingArticleSchema) {
    existingArticleSchema.remove()
  }
  
  const articleSchema = {
    "@context": "https://schema.org",
    "@type": "BlogPosting",
    "headline": blogData.title,
    "description": blogData.excerpt,
    "image": "https://rayso.ai/blog/" + blogData.id + ".jpg",
    "datePublished": blogData.date,
    "dateModified": blogData.date,
    "author": {
      "@type": "Organization",
      "name": blogData.author,
      "url": "https://rayso.ai"
    },
    "publisher": {
      "@type": "Organization",
      "name": "瑞幻智能",
      "alternateName": "RaySo.AI",
      "logo": {
        "@type": "ImageObject",
        "url": "https://rayso.ai/logo.png"
      }
    },
    "mainEntityOfPage": {
      "@type": "WebPage",
      "@id": "https://rayso.ai/blog/" + blogData.id
    },
    "articleSection": blogData.category,
    "keywords": blogData.tags.join(", ")
  }
  
  const schemaScript = document.createElement('script')
  schemaScript.type = 'application/ld+json'
  schemaScript.id = 'blog-article-schema'
  schemaScript.textContent = JSON.stringify(articleSchema)
  document.head.appendChild(schemaScript)
  
  // 更新面包屑导航
  const existingBreadcrumb = document.getElementById('blog-detail-breadcrumb')
  if (existingBreadcrumb) {
    existingBreadcrumb.remove()
  }
  
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
      },
      {
        "@type": "ListItem",
        "position": 3,
        "name": blogData.title,
        "item": "https://rayso.ai/blog/" + blogData.id
      }
    ]
  }
  
  const breadcrumbScript = document.createElement('script')
  breadcrumbScript.type = 'application/ld+json'
  breadcrumbScript.id = 'blog-detail-breadcrumb'
  breadcrumbScript.textContent = JSON.stringify(breadcrumbSchema)
  document.head.appendChild(breadcrumbScript)
}

// 从路由参数获取 blogId
onMounted(() => {
  // 优先从 window.blogDetailId 获取（从 BlogPage 传递）
  if (window.blogDetailId) {
    blogId.value = window.blogDetailId
    blog.value = blogArticles.find(b => b.id === blogId.value)
    window.blogDetailId = null
  } else {
    // 从 URL hash 获取 blogId
    const hash = window.location.hash
    if (hash) {
      const match = hash.match(/blogId=(\d+)/)
      if (match) {
        blogId.value = parseInt(match[1])
        blog.value = blogArticles.find(b => b.id === blogId.value)
      }
    }
  }
  
  // 更新 SEO
  if (blog.value) {
    updateBlogSEO(blog.value)
  }
  
  // 渲染内容后高亮代码
  nextTick(() => {
    if (window.hljs) {
      document.querySelectorAll('.article-content pre code').forEach((block) => {
        window.hljs.highlightElement(block)
      })
    }
  })
})

// 监听 blog 变化，更新 SEO
watch(blog, (newBlog) => {
  if (newBlog) {
    updateBlogSEO(newBlog)
  }
})

const renderedContent = computed(() => {
  if (!blog.value) return ''
  
  // 使用 marked 解析 Markdown
  if (window.marked) {
    return window.marked.parse(blog.value.content)
  }
  return blog.value.content
})

const goBack = () => {
  navigate('blog')
}

// 接收从 App.vue 传递的参数（如果需要）
const props = defineProps({
  blogId: {
    type: Number,
    default: null
  }
})

// 监听 props 变化
if (props.blogId && !blog.value) {
  blogId.value = props.blogId
  blog.value = blogArticles.find(b => b.id === props.blogId)
}
</script>

<style scoped>
.blog-detail-page {
  min-height: calc(100vh - 80px);
  margin-top: 80px;
}

.blog-detail-section {
  padding: 100px 40px;
  background: #FFFFFF;
}

.blog-detail-container {
  max-width: 900px;
  margin: 0 auto;
}

.back-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 20px;
  background: #F5F5F7;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  color: #1D1D1F;
  cursor: pointer;
  margin-bottom: 30px;
  transition: all 0.3s;
}

.back-btn:hover {
  background: #E5E5E7;
  color: #1D4ED8;
}

.blog-article {
  background: #FFFFFF;
  border-radius: 16px;
  padding: 40px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
}

.article-header {
  margin-bottom: 40px;
  padding-bottom: 24px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.article-category {
  display: inline-block;
  background: #1D4ED8;
  color: #FFFFFF;
  padding: 6px 16px;
  border-radius: 12px;
  font-size: 13px;
  font-weight: 600;
  margin-bottom: 16px;
}

.article-title {
  font-size: 36px;
  font-weight: 700;
  color: #1D1D1F;
  margin-bottom: 16px;
  line-height: 1.3;
}

.article-meta {
  display: flex;
  align-items: center;
  gap: 20px;
  font-size: 14px;
  color: #6E6E73;
}

.article-meta span {
  display: flex;
  align-items: center;
  gap: 6px;
}

.article-tags {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-top: 16px;
}

.article-tag {
  font-size: 12px;
  color: #1D4ED8;
  background: rgba(29, 78, 216, 0.1);
  padding: 4px 12px;
  border-radius: 12px;
}

.article-content {
  font-size: 16px;
  line-height: 1.8;
  color: #1D1D1F;
}

.article-content :deep(h1),
.article-content :deep(h2),
.article-content :deep(h3),
.article-content :deep(h4) {
  margin-top: 32px;
  margin-bottom: 16px;
  color: #1D1D1F;
  font-weight: 600;
}

.article-content :deep(h1) {
  font-size: 28px;
}

.article-content :deep(h2) {
  font-size: 24px;
}

.article-content :deep(h3) {
  font-size: 20px;
}

.article-content :deep(p) {
  margin-bottom: 16px;
}

.article-content :deep(ul),
.article-content :deep(ol) {
  margin-bottom: 16px;
  padding-left: 24px;
}

.article-content :deep(li) {
  margin-bottom: 8px;
}

.article-content :deep(code) {
  background: #F5F5F7;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 14px;
  font-family: 'Courier New', monospace;
  color: #E83E8C;
}

.article-content :deep(pre) {
  background: #F5F5F7;
  padding: 20px;
  border-radius: 8px;
  overflow-x: auto;
  margin-bottom: 20px;
}

.article-content :deep(pre code) {
  background: none;
  padding: 0;
  color: inherit;
  font-size: 14px;
}

.article-content :deep(blockquote) {
  border-left: 4px solid #1D4ED8;
  padding-left: 20px;
  margin: 20px 0;
  color: #6E6E73;
  font-style: italic;
}

.article-content :deep(table) {
  width: 100%;
  border-collapse: collapse;
  margin: 20px 0;
}

.article-content :deep(table th),
.article-content :deep(table td) {
  border: 1px solid #E5E5E7;
  padding: 12px;
  text-align: left;
}

.article-content :deep(table th) {
  background: #F5F5F7;
  font-weight: 600;
}

.article-content :deep(img) {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
  margin: 20px 0;
}

.article-content :deep(a) {
  color: #1D4ED8;
  text-decoration: none;
}

.article-content :deep(a:hover) {
  text-decoration: underline;
}

.loading-state {
  text-align: center;
  padding: 60px;
  color: #6E6E73;
}

@media (max-width: 768px) {
  .blog-detail-section {
    padding: 40px 20px;
  }

  .blog-article {
    padding: 24px;
  }

  .article-title {
    font-size: 24px;
  }

  .article-content {
    font-size: 14px;
  }

  .article-content :deep(h1) {
    font-size: 22px;
  }

  .article-content :deep(h2) {
    font-size: 20px;
  }

  .article-content :deep(h3) {
    font-size: 18px;
  }
}
</style>

