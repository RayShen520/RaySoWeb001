<template>
  <div class="home-page">
    <section class="hero">
      <h1>全球领先的AI智能解决方案提供商<sup style="font-size: 0.4em; vertical-align: super;">*</sup></h1>
      <p>专注于AI全网营销、智能体应用、自动化开发与视觉检测的创新科技公司</p>
      <a href="#" @click.prevent="goToContact" class="cta-button">立即咨询</a>
    </section>

    <section class="services">
      <h2 class="section-title">核心业务</h2>
      <div class="services-grid">
        <div 
          v-for="service in services" 
          :key="service.id"
          class="service-card"
        >
          <div class="service-icon">{{ service.icon }}</div>
          <h3>{{ service.title }}</h3>
          <p>{{ service.description }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { inject } from 'vue'

const navigate = inject('navigate')

const services = [
  { id: 1, icon: '🚀', title: 'AI全网营销', description: '智能化的全网营销解决方案，提升品牌影响力' },
  { id: 2, icon: '🤖', title: 'AI智能体应用', description: '构建智能化的AI智能体应用系统' },
  { id: 3, icon: '⚙️', title: 'AI自动化开发', description: '高效的AI自动化开发工具与服务' },
  { id: 4, icon: '👁️', title: 'AI视觉检测', description: '精准的AI视觉检测技术应用' }
]

const goToContact = () => {
  navigate('contact')
}
</script>

<style scoped>
.home-page {
    min-height: calc(100vh - 80px);
    margin-top: 80px;
}

.hero {
    padding: 120px 40px;
    text-align: center;
    background: linear-gradient(135deg, #F5F5F7 0%, #FFFFFF 100%);
}

.hero h1 {
    font-size: 64px;
    font-weight: 700;
    margin-bottom: 24px;
    color: #1D1D1F;
    animation: fadeInUp 0.8s ease-out;
}

.hero p {
    font-size: 24px;
    color: #6E6E73;
    margin-bottom: 40px;
    max-width: 800px;
    margin-left: auto;
    margin-right: auto;
    animation: fadeInUp 0.8s ease-out 0.2s both;
}

.cta-button {
    display: inline-block;
    padding: 16px 40px;
    background: #1D4ED8;
    color: #FFFFFF;
    text-decoration: none;
    border-radius: 8px;
    font-size: 18px;
    font-weight: 600;
    transition: background 0.3s, transform 0.3s;
    animation: fadeInUp 0.8s ease-out 0.4s both;
    cursor: pointer;
    border: none;
}

.cta-button:hover {
    background: #1E40AF;
    transform: translateY(-2px);
}

.services {
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

.services-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.service-card {
    background: #F5F5F7;
    border: 1px solid rgba(0, 0, 0, 0.05);
    border-radius: 16px;
    padding: 40px;
    text-align: center;
    transition: transform 0.3s, box-shadow 0.3s;
}

.service-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.service-icon {
    width: 80px;
    height: 80px;
    background: linear-gradient(135deg, #1D4ED8 0%, #0066CC 100%);
    border-radius: 50%;
    margin: 0 auto 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 32px;
}

.service-card h3 {
    font-size: 24px;
    margin-bottom: 16px;
    color: #1D4ED8;
}

.service-card p {
    color: #6E6E73;
    font-size: 16px;
}

@media (max-width: 768px) {
    .hero h1 {
        font-size: 36px;
    }

    .hero p {
        font-size: 18px;
    }

    .services-grid {
        grid-template-columns: 1fr;
    }
}
</style>

