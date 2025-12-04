<template>
  <div class="products-page">
    <section class="products-section">
      <h2 class="section-title">产品与服务</h2>
      
      <div 
        v-for="(product, index) in products" 
        :key="product.id"
        class="product-detail"
        :class="{ 'reverse': index % 2 === 1 }"
      >
        <div class="product-image">{{ product.icon }}</div>
        <div class="product-content">
          <h3>{{ product.title }}</h3>
          <p>{{ product.description }}</p>
          <ul class="product-features">
            <li v-for="feature in product.features" :key="feature">{{ feature }}</li>
          </ul>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
const products = [
  {
    id: 1,
    icon: '🚀',
    title: 'AI全网营销',
    description: '基于人工智能技术的全网营销解决方案，帮助企业实现精准营销、提升品牌影响力。通过智能分析和自动化工具，优化营销策略，提高转化率。',
    features: [
      '智能数据分析与用户画像',
      '自动化内容创作与发布',
      '多渠道营销整合',
      '实时效果监控与优化'
    ]
  },
  {
    id: 2,
    icon: '🤖',
    title: 'AI智能体应用',
    description: '构建企业级AI智能体应用系统，实现业务流程自动化、智能决策支持。提供定制化的智能体解决方案，满足不同行业需求。',
    features: [
      '智能对话与客服系统',
      '业务流程自动化',
      '智能决策支持',
      '多场景应用适配'
    ]
  },
  {
    id: 3,
    icon: '⚙️',
    title: 'AI自动化开发',
    description: '提供高效的AI自动化开发工具与服务，加速软件开发流程，降低开发成本。支持代码生成、测试自动化、部署自动化等功能。',
    features: [
      '智能代码生成',
      '自动化测试框架',
      'CI/CD自动化部署',
      '开发效率提升工具'
    ]
  },
  {
    id: 4,
    icon: '👁️',
    title: 'AI视觉检测',
    description: '精准的AI视觉检测技术应用，适用于工业质检、安全监控、医疗影像等多个领域。提供高精度的图像识别与分析服务。',
    features: [
      '高精度图像识别',
      '实时检测与分析',
      '多场景应用支持',
      '定制化检测方案'
    ]
  }
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
    background: #F5F5F7;
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 80px;
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

@media (max-width: 768px) {
    .product-detail {
        grid-template-columns: 1fr;
        gap: 30px;
    }

    .product-detail.reverse {
        direction: ltr;
    }
}
</style>

