<template>
  <div class="products-page">
    <main>
    <section class="products-section">
      <h1 class="section-title">瑞幻智能 - 产品与服务</h1>
      
      <article 
        v-for="(product, index) in products" 
        :key="product.id"
        class="product-detail"
        :class="{ 'reverse': index % 2 === 1 }"
      >
        <div class="product-image" :aria-label="product.title + '产品图标'" role="img">{{ product.icon }}</div>
        <div class="product-content">
          <h3>{{ product.title }}</h3>
          <p>{{ product.description }}</p>
          <ul class="product-features">
            <li v-for="feature in product.features" :key="feature">{{ feature }}</li>
          </ul>
          <div class="product-specs">
            <div class="specs-title">核心参数</div>
            <div class="specs-grid">
              <div 
                v-for="spec in product.specs" 
                :key="spec.label"
                class="spec-item"
              >
                <span class="spec-label">{{ spec.label }}</span>
                <span class="spec-value">{{ spec.value }}</span>
              </div>
            </div>
          </div>
          <div class="product-scenarios">
            <div class="scenarios-title">应用场景</div>
            <div class="scenarios-list">
              <span 
                v-for="scenario in product.scenarios" 
                :key="scenario"
                class="scenario-tag"
              >
                {{ scenario }}
              </span>
            </div>
          </div>
          <div class="product-cta">
            <a href="#" @click.prevent="goToContact" class="product-btn" :aria-label="'咨询' + product.title + '服务'">立即咨询</a>
          </div>
        </div>
      </article>
    </section>

    <!-- 产品对比区域 -->
    <section class="comparison-section">
      <h2 class="section-title">产品方案对比</h2>
      <div class="comparison-table">
        <table>
          <thead>
            <tr>
              <th>功能特性</th>
              <th>基础版</th>
              <th>专业版</th>
              <th>企业版</th>
            </tr>
          </thead>
          <tbody>
            <tr 
              v-for="row in comparisonData" 
              :key="row.feature"
            >
              <td>{{ row.feature }}</td>
              <td>{{ row.basic }}</td>
              <td>{{ row.professional }}</td>
              <td>{{ row.enterprise }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>
    </main>
  </div>
</template>

<script setup>
import { inject, onMounted } from 'vue'

const navigate = inject('navigate')

// 添加面包屑导航结构化数据
onMounted(() => {
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
        "name": "产品服务",
        "item": "https://rayso.ai/products"
      }
    ]
  }
  
  let existingSchema = document.getElementById('products-breadcrumb-schema')
  if (!existingSchema) {
    const schemaScript = document.createElement('script')
    schemaScript.type = 'application/ld+json'
    schemaScript.id = 'products-breadcrumb-schema'
    schemaScript.textContent = JSON.stringify(breadcrumbSchema)
    document.head.appendChild(schemaScript)
  }
})

const goToContact = () => {
  navigate('contact')
}

const products = [
  {
    id: 1,
    icon: '🚀',
    title: 'AI全网营销',
    description: '瑞幻智能基于人工智能技术的全网营销解决方案，帮助企业实现精准营销、提升品牌影响力。瑞幻智能通过智能分析和自动化工具，优化营销策略，提高转化率。',
    features: [
      '智能数据分析与用户画像',
      '自动化内容创作与发布',
      '多渠道营销整合',
      '实时效果监控与优化'
    ],
    specs: [
      { label: '支持平台', value: '50+' },
      { label: '日处理量', value: '100万+' },
      { label: '响应速度', value: '<100ms' },
      { label: '准确率', value: '95%+' }
    ],
    scenarios: ['电商营销', '品牌推广', '内容营销', '社交媒体']
  },
  {
    id: 2,
    icon: '🤖',
    title: 'AI智能体应用',
    description: '瑞幻智能构建企业级AI智能体应用系统，实现业务流程自动化、智能决策支持。瑞幻智能提供定制化的智能体解决方案，满足不同行业需求。',
    features: [
      '智能对话与客服系统',
      '业务流程自动化',
      '智能决策支持',
      '多场景应用适配'
    ],
    specs: [
      { label: '并发支持', value: '10,000+' },
      { label: '响应时间', value: '<200ms' },
      { label: '理解准确率', value: '98%+' },
      { label: '支持语言', value: '20+' }
    ],
    scenarios: ['智能客服', '业务助手', '数据分析', '决策支持']
  },
  {
    id: 3,
    icon: '⚙️',
    title: 'AI自动化开发',
    description: '瑞幻智能提供高效的AI自动化开发工具与服务，加速软件开发流程，降低开发成本。瑞幻智能支持代码生成、测试自动化、部署自动化等功能。',
    features: [
      '智能代码生成',
      '自动化测试框架',
      'CI/CD自动化部署',
      '开发效率提升工具'
    ],
    specs: [
      { label: '代码生成率', value: '60%+' },
      { label: '效率提升', value: '3-5倍' },
      { label: '支持语言', value: '15+' },
      { label: '测试覆盖率', value: '90%+' }
    ],
    scenarios: ['快速开发', '代码审查', '自动化测试', '持续集成']
  },
  {
    id: 4,
    icon: '👁️',
    title: 'AI视觉检测',
    description: '瑞幻智能提供精准的AI视觉检测技术应用，适用于工业质检、安全监控、医疗影像等多个领域。瑞幻智能提供高精度的图像识别与分析服务。',
    features: [
      '高精度图像识别',
      '实时检测与分析',
      '多场景应用支持',
      '定制化检测方案'
    ],
    specs: [
      { label: '检测准确率', value: '99.8%' },
      { label: '处理速度', value: '<50ms' },
      { label: '支持分辨率', value: '4K+' },
      { label: '识别类别', value: '1000+' }
    ],
    scenarios: ['工业质检', '安全监控', '医疗影像', '智能识别']
  }
]

const comparisonData = [
  { feature: 'AI模型数量', basic: '5个', professional: '20个', enterprise: '无限' },
  { feature: 'API调用次数/月', basic: '10万', professional: '100万', enterprise: '无限' },
  { feature: '数据存储', basic: '10GB', professional: '100GB', enterprise: '无限' },
  { feature: '技术支持', basic: '邮件支持', professional: '7×24小时', enterprise: '专属顾问' },
  { feature: '定制开发', basic: '—', professional: '✓', enterprise: '✓' },
  { feature: '私有化部署', basic: '—', professional: '—', enterprise: '✓' },
  { feature: 'SLA保障', basic: '99%', professional: '99.9%', enterprise: '99.99%' }
]
</script>

<style scoped>
.products-page {
    min-height: calc(100vh - 80px);
    margin-top: 80px;
}

.products-section {
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

.product-detail {
    max-width: 1200px;
    margin: 0 auto 80px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px;
    align-items: center;
}

.product-detail.reverse {
    direction: rtl;
}

.product-detail.reverse > * {
    direction: ltr;
}

.product-image {
    width: 100%;
    height: 400px;
    background: linear-gradient(135deg, #F5F5F7 0%, #E5E5E7 100%);
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 80px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
}

.product-content h3 {
    font-size: 36px;
    color: #1D4ED8;
    margin-bottom: 20px;
}

.product-content p {
    font-size: 18px;
    color: #6E6E73;
    margin-bottom: 16px;
    line-height: 1.8;
}

.product-features {
    list-style: none;
    margin-top: 24px;
}

.product-features li {
    padding: 12px 0;
    color: #1D1D1F;
    font-size: 16px;
    position: relative;
    padding-left: 24px;
}

.product-features li::before {
    content: '✓';
    position: absolute;
    left: 0;
    color: #1D4ED8;
    font-weight: bold;
}

.product-specs {
    margin-top: 30px;
    padding: 24px;
    background: #F5F5F7;
    border-radius: 12px;
}

.specs-title {
    font-size: 18px;
    font-weight: 600;
    color: #1D1D1F;
    margin-bottom: 16px;
}

.specs-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
}

.spec-item {
    display: flex;
    justify-content: space-between;
    padding: 8px 0;
    border-bottom: 1px solid rgba(0, 0, 0, 0.05);
}

.spec-label {
    font-size: 14px;
    color: #6E6E73;
}

.spec-value {
    font-size: 14px;
    font-weight: 600;
    color: #1D1D1F;
}

.product-scenarios {
    margin-top: 30px;
}

.scenarios-title {
    font-size: 18px;
    font-weight: 600;
    color: #1D1D1F;
    margin-bottom: 16px;
}

.scenarios-list {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
}

.scenario-tag {
    display: inline-block;
    padding: 6px 16px;
    background: #FFFFFF;
    border: 1px solid #E5E5E7;
    border-radius: 20px;
    font-size: 14px;
    color: #1D1D1F;
    transition: all 0.3s;
}

.scenario-tag:hover {
    background: #1D4ED8;
    color: #FFFFFF;
    border-color: #1D4ED8;
}

.product-cta {
    margin-top: 30px;
}

.product-btn {
    display: inline-block;
    padding: 12px 32px;
    background: #1D4ED8;
    color: #FFFFFF;
    text-decoration: none;
    border-radius: 8px;
    font-size: 16px;
    font-weight: 600;
    transition: background 0.3s, transform 0.3s;
}

.product-btn:hover {
    background: #1E40AF;
    transform: translateY(-2px);
}

/* 产品对比区域 */
.comparison-section {
    padding: 100px 40px;
    background: #F5F5F7;
}

.comparison-table {
    max-width: 1200px;
    margin: 0 auto;
    background: #FFFFFF;
    border-radius: 16px;
    overflow: hidden;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
}

.comparison-table table {
    width: 100%;
    border-collapse: collapse;
}

.comparison-table th {
    background: #1D4ED8;
    color: #FFFFFF;
    padding: 20px;
    text-align: left;
    font-weight: 600;
}

.comparison-table td {
    padding: 16px 20px;
    border-bottom: 1px solid #F5F5F7;
}

.comparison-table tr:last-child td {
    border-bottom: none;
}

.comparison-table tr:hover {
    background: #F5F5F7;
}

.comparison-table .check-mark {
    color: #1D4ED8;
    font-weight: bold;
}

@media (max-width: 768px) {
    /* 区域 padding 优化 */
    .products-section,
    .comparison-section {
        padding: 40px 20px;
    }

    /* 标题优化 */
    .section-title {
        font-size: 32px;
        margin-bottom: 30px;
    }

    .product-detail {
        grid-template-columns: 1fr;
        gap: 24px;
        margin-bottom: 50px;
    }

    .product-detail.reverse {
        direction: ltr;
    }

    .product-image {
        height: 250px;
        font-size: 60px;
    }

    .product-content h3 {
        font-size: 24px;
        margin-bottom: 16px;
    }

    .product-content p {
        font-size: 16px;
        margin-bottom: 12px;
    }

    .product-features {
        margin-top: 16px;
    }

    .product-features li {
        padding: 8px 0;
        font-size: 14px;
        padding-left: 20px;
    }

    .product-specs {
        margin-top: 20px;
        padding: 20px;
    }

    .specs-title {
        font-size: 16px;
        margin-bottom: 12px;
    }

    .specs-grid {
        grid-template-columns: 1fr;
        gap: 8px;
    }

    .spec-item {
        padding: 6px 0;
    }

    .spec-label,
    .spec-value {
        font-size: 13px;
    }

    .product-scenarios {
        margin-top: 20px;
    }

    .scenarios-title {
        font-size: 16px;
        margin-bottom: 12px;
    }

    .scenarios-list {
        gap: 8px;
    }

    .scenario-tag {
        padding: 5px 12px;
        font-size: 12px;
    }

    .product-cta {
        margin-top: 20px;
    }

    .product-btn {
        padding: 10px 24px;
        font-size: 14px;
    }

    .comparison-table {
        overflow-x: auto;
    }

    .comparison-table table {
        min-width: 600px;
    }

    .comparison-table th,
    .comparison-table td {
        padding: 12px 16px;
        font-size: 14px;
    }
}
</style>

