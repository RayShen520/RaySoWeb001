<template>
  <div class="home-page">
    <section class="hero">
      <h1>全球领先的AI智能解决方案提供商<sup style="font-size: 0.4em; vertical-align: super;">*</sup></h1>
      <p>专注于AI全网营销、智能体应用、自动化开发与视觉检测的创新科技公司</p>
      <a href="#" @click.prevent="goToContact" class="cta-button">立即咨询</a>
    </section>

    <!-- 统计数据区域 -->
    <section class="stats-section">
      <div class="stats-grid">
        <div 
          v-for="stat in stats" 
          :key="stat.id"
          class="stat-card"
        >
          <div class="stat-title">{{ stat.title }}</div>
          <div class="stat-value">{{ stat.value }}</div>
          <div class="stat-desc">{{ stat.desc }}</div>
        </div>
      </div>
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

    <!-- 认证资质区域 -->
    <section class="certifications-section">
      <h2 class="section-title">资质认证</h2>
      <div class="cert-grid">
        <div 
          v-for="cert in certifications" 
          :key="cert.id"
          class="cert-item"
        >
          <div class="cert-badge">{{ cert.badge }}</div>
          <div class="cert-name">{{ cert.name }}</div>
          <div class="cert-desc">{{ cert.desc }}</div>
        </div>
      </div>
    </section>

    <!-- 优势特色区域 -->
    <section class="features-section">
      <h2 class="section-title">核心优势</h2>
      <div class="features-grid">
        <div 
          v-for="feature in features" 
          :key="feature.id"
          class="feature-item"
        >
          <div class="feature-icon">{{ feature.icon }}</div>
          <h3>{{ feature.title }}</h3>
          <p>{{ feature.description }}</p>
        </div>
      </div>
    </section>

    <!-- 客户案例区域 -->
    <section class="clients-section">
      <h2 class="section-title">合作伙伴</h2>
      <div class="clients-grid">
        <div 
          v-for="client in clients" 
          :key="client.id"
          class="client-logo"
        >
          {{ client.name }}
        </div>
      </div>
    </section>

    <!-- 客户评价区域 -->
    <section class="testimonials-section">
      <h2 class="section-title">客户评价</h2>
      <div class="testimonials-grid">
        <div 
          v-for="testimonial in testimonials" 
          :key="testimonial.id"
          class="testimonial-card"
        >
          <div class="testimonial-rating">{{ testimonial.rating }}</div>
          <div class="testimonial-content">{{ testimonial.content }}</div>
          <div class="testimonial-author">
            <div class="author-avatar">{{ testimonial.authorInitial }}</div>
            <div class="author-info">
              <h4>{{ testimonial.authorName }}</h4>
              <p>{{ testimonial.authorTitle }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 服务流程区域 -->
    <section class="process-section">
      <h2 class="section-title">服务流程</h2>
      <div class="process-steps">
        <div 
          v-for="step in processSteps" 
          :key="step.id"
          class="process-step"
        >
          <div class="step-number">{{ step.number }}</div>
          <div class="step-title">{{ step.title }}</div>
          <div class="step-desc">{{ step.desc }}</div>
        </div>
      </div>
    </section>

    <!-- 技术优势区域 -->
    <section class="tech-section">
      <h2 class="section-title">技术优势</h2>
      <div class="tech-list">
        <div 
          v-for="tech in techList" 
          :key="tech"
          class="tech-item"
        >
          <div class="tech-name">{{ tech }}</div>
        </div>
      </div>
    </section>

    <!-- 成功案例区域 -->
    <section class="cases-section">
      <h2 class="section-title">成功案例</h2>
      <div class="cases-grid">
        <div 
          v-for="caseItem in cases" 
          :key="caseItem.id"
          class="case-card"
        >
          <div class="case-image">{{ caseItem.icon }}</div>
          <div class="case-content">
            <span class="case-tag">{{ caseItem.tag }}</span>
            <h3 class="case-title">{{ caseItem.title }}</h3>
            <p class="case-desc">{{ caseItem.desc }}</p>
            <div class="case-result">
              <div 
                v-for="result in caseItem.results" 
                :key="result.label"
                class="result-item"
              >
                <div class="result-value">{{ result.value }}</div>
                <div class="result-label">{{ result.label }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 新闻动态区域 -->
    <section class="news-section">
      <h2 class="section-title">最新动态</h2>
      <div class="news-grid">
        <div 
          v-for="news in newsList" 
          :key="news.id"
          class="news-card"
        >
          <div class="news-date">{{ news.date }}</div>
          <div class="news-content">
            <h3 class="news-title">{{ news.title }}</h3>
            <p class="news-excerpt">{{ news.excerpt }}</p>
            <a href="#" class="news-link">了解更多 →</a>
          </div>
        </div>
      </div>
    </section>

    <!-- 行业解决方案区域 -->
    <section class="industries-section">
      <h2 class="section-title">行业解决方案</h2>
      <div class="industries-grid">
        <div 
          v-for="industry in industries" 
          :key="industry.id"
          class="industry-card"
        >
          <div class="industry-icon">{{ industry.icon }}</div>
          <h3 class="industry-name">{{ industry.name }}</h3>
          <p class="industry-desc">{{ industry.desc }}</p>
        </div>
      </div>
    </section>

    <!-- 奖项荣誉区域 -->
    <section class="awards-section">
      <h2 class="section-title">荣誉奖项</h2>
      <div class="awards-grid">
        <div 
          v-for="award in awards" 
          :key="award.id"
          class="award-item"
        >
          <div class="award-icon">{{ award.icon }}</div>
          <div class="award-name">{{ award.name }}</div>
          <div class="award-year">{{ award.year }}</div>
        </div>
      </div>
    </section>

    <!-- 团队介绍区域 -->
    <section class="team-section">
      <h2 class="section-title">核心团队</h2>
      <div class="team-grid">
        <div 
          v-for="member in teamMembers" 
          :key="member.id"
          class="team-card"
        >
          <div class="team-avatar">{{ member.initial }}</div>
          <h3>{{ member.name }}</h3>
          <p class="team-role">{{ member.role }}</p>
          <p class="team-desc">{{ member.desc }}</p>
        </div>
      </div>
    </section>

    <!-- 技术架构区域 -->
    <section class="tech-arch-section">
      <h2 class="section-title">技术架构</h2>
      <div class="tech-arch-grid">
        <div 
          v-for="arch in techArch" 
          :key="arch.id"
          class="tech-arch-card"
        >
          <div class="tech-arch-icon">{{ arch.icon }}</div>
          <h3>{{ arch.title }}</h3>
          <p>{{ arch.desc }}</p>
        </div>
      </div>
    </section>

    <!-- 加入我们区域 -->
    <section class="joinus-section">
      <div class="joinus-content">
        <h2>加入我们</h2>
        <p>我们正在寻找对AI技术充满热情的优秀人才，一起推动人工智能技术的创新与发展</p>
        <a href="#" @click.prevent="goToContact" class="joinus-button">立即加入</a>
      </div>
    </section>
  </div>
</template>

<script setup>
import { inject } from 'vue'

const navigate = inject('navigate')

const stats = [
  { id: 1, title: '企业客户', value: '120+', desc: '覆盖12个行业' },
  { id: 2, title: '上线终端', value: '48,000', desc: '全球42城运行' },
  { id: 3, title: '模型更新', value: '72h', desc: '自动安全审核' },
  { id: 4, title: '满意度', value: '98%', desc: 'NPS 67分' }
]

const services = [
  { id: 1, icon: '🚀', title: 'AI全网营销', description: '智能化的全网营销解决方案，提升品牌影响力' },
  { id: 2, icon: '🤖', title: 'AI智能体应用', description: '构建智能化的AI智能体应用系统' },
  { id: 3, icon: '⚙️', title: 'AI自动化开发', description: '高效的AI自动化开发工具与服务' },
  { id: 4, icon: '👁️', title: 'AI视觉检测', description: '精准的AI视觉检测技术应用' }
]

const certifications = [
  { id: 1, badge: 'ISO', name: 'ISO 27001', desc: '信息安全管理体系认证' },
  { id: 2, badge: 'CMMI', name: 'CMMI 5级', desc: '软件能力成熟度模型' },
  { id: 3, badge: 'AI', name: 'AI能力认证', desc: '人工智能企业认证' },
  { id: 4, badge: '高企', name: '高新技术企业', desc: '国家高新技术企业认定' },
  { id: 5, badge: '软著', name: '软件著作权', desc: '50+项软件著作权' },
  { id: 6, badge: '专利', name: '发明专利', desc: '30+项AI相关专利' }
]

const features = [
  { id: 1, icon: '🔒', title: '数据安全', description: '通过ISO 27001认证，采用企业级加密技术，确保客户数据安全无忧' },
  { id: 2, icon: '⚡', title: '极速响应', description: '全球CDN加速，毫秒级响应，支持高并发访问，保障业务稳定运行' },
  { id: 3, icon: '🎯', title: '精准智能', description: '基于深度学习算法，AI模型准确率达98%以上，持续优化升级' },
  { id: 4, icon: '🌐', title: '全球服务', description: '覆盖42个城市，7×24小时技术支持，多语言服务团队' },
  { id: 5, icon: '🔄', title: '持续创新', description: '72小时模型更新周期，快速响应市场变化，保持技术领先' },
  { id: 6, icon: '🤝', title: '专业服务', description: '98%客户满意度，NPS 67分，一对一专属顾问，全程跟踪服务' }
]

const clients = [
  { id: 1, name: '华为' },
  { id: 2, name: '腾讯' },
  { id: 3, name: '阿里巴巴' },
  { id: 4, name: '字节跳动' },
  { id: 5, name: '京东' },
  { id: 6, name: '小米' }
]

const testimonials = [
  {
    id: 1,
    rating: '★★★★★',
    content: '瑞幻智能的AI解决方案帮助我们提升了30%的营销转化率，服务专业，响应迅速，强烈推荐！',
    authorInitial: '张',
    authorName: '张总',
    authorTitle: '某知名科技公司 CEO'
  },
  {
    id: 2,
    rating: '★★★★★',
    content: 'AI自动化开发工具大大提升了我们的开发效率，项目交付时间缩短了40%，团队非常满意。',
    authorInitial: '李',
    authorName: '李经理',
    authorTitle: '某互联网公司 CTO'
  },
  {
    id: 3,
    rating: '★★★★★',
    content: '视觉检测系统准确率非常高，帮助我们实现了生产线的智能化升级，成本降低了25%。',
    authorInitial: '王',
    authorName: '王总监',
    authorTitle: '某制造企业 技术总监'
  }
]

const processSteps = [
  { id: 1, number: 1, title: '需求分析', desc: '深入了解业务需求，制定个性化解决方案' },
  { id: 2, number: 2, title: '方案设计', desc: '专业团队设计技术方案，确保可行性' },
  { id: 3, number: 3, title: '开发实施', desc: '敏捷开发，快速迭代，确保项目进度' },
  { id: 4, number: 4, title: '测试验收', desc: '严格测试，确保质量，客户验收' },
  { id: 5, number: 5, title: '上线运维', desc: '平稳上线，7×24小时监控，持续优化' }
]

const techList = [
  '深度学习',
  '机器学习',
  '自然语言处理',
  '计算机视觉',
  '知识图谱',
  '强化学习',
  '联邦学习',
  '边缘计算',
  '云计算',
  '大数据分析',
  '区块链',
  '物联网'
]

const cases = [
  {
    id: 1,
    icon: '🏢',
    tag: '金融行业',
    title: '某大型银行智能客服系统',
    desc: '通过AI智能体应用，实现7×24小时智能客服，处理效率提升300%，客户满意度达到95%以上。',
    results: [
      { value: '300%', label: '效率提升' },
      { value: '95%', label: '满意度' }
    ]
  },
  {
    id: 2,
    icon: '🏭',
    tag: '制造业',
    title: '智能制造视觉检测平台',
    desc: '部署AI视觉检测系统，实现生产线自动化质检，准确率达99.8%，不良品率降低80%。',
    results: [
      { value: '99.8%', label: '检测准确率' },
      { value: '80%', label: '不良品降低' }
    ]
  },
  {
    id: 3,
    icon: '🛒',
    tag: '电商行业',
    title: '电商平台AI营销解决方案',
    desc: '运用AI全网营销技术，实现精准用户画像和个性化推荐，转化率提升45%，ROI提升200%。',
    results: [
      { value: '45%', label: '转化率提升' },
      { value: '200%', label: 'ROI提升' }
    ]
  }
]

const newsList = [
  {
    id: 1,
    date: '2024-12-04',
    title: '瑞幻智能荣获"2024年度AI创新企业"大奖',
    excerpt: '在2024年度AI创新峰会上，瑞幻智能凭借在AI智能体应用领域的卓越表现，荣获"年度AI创新企业"称号...'
  },
  {
    id: 2,
    date: '2024-11-28',
    title: '全新AI自动化开发平台正式上线',
    excerpt: '经过6个月的研发和测试，瑞幻智能全新AI自动化开发平台正式上线，支持多种编程语言和框架...'
  },
  {
    id: 3,
    date: '2024-11-15',
    title: '与华为云达成战略合作，共建AI生态',
    excerpt: '瑞幻智能与华为云签署战略合作协议，双方将在AI技术、云计算服务等领域展开深度合作...'
  }
]

const industries = [
  { id: 1, icon: '🏦', name: '金融科技', desc: '智能风控、反欺诈、智能投顾等金融AI解决方案' },
  { id: 2, icon: '🏥', name: '医疗健康', desc: '医学影像分析、智能诊断、健康管理等AI应用' },
  { id: 3, icon: '🏭', name: '智能制造', desc: '工业视觉检测、预测性维护、质量管控系统' },
  { id: 4, icon: '🛒', name: '零售电商', desc: '智能推荐、精准营销、供应链优化解决方案' },
  { id: 5, icon: '🎓', name: '教育培训', desc: '智能教学、个性化学习、知识图谱构建' },
  { id: 6, icon: '🚗', name: '智慧交通', desc: '智能调度、路况预测、自动驾驶技术支持' }
]

const awards = [
  { id: 1, icon: '🏆', name: 'AI创新企业奖', year: '2024年' },
  { id: 2, icon: '⭐', name: '最佳AI解决方案', year: '2024年' },
  { id: 3, icon: '🎖️', name: '科技创新奖', year: '2023年' },
  { id: 4, icon: '💎', name: '优秀服务商', year: '2023年' },
  { id: 5, icon: '🌟', name: '行业标杆企业', year: '2023年' },
  { id: 6, icon: '🎯', name: '客户满意度第一', year: '2022年' }
]

const teamMembers = [
  { id: 1, initial: '张', name: '张总', role: 'CEO & 创始人', desc: '15年AI行业经验，前BAT技术专家' },
  { id: 2, initial: '李', name: '李博士', role: 'CTO & 技术总监', desc: '清华大学AI博士，发表论文50+篇' },
  { id: 3, initial: '王', name: '王总', role: 'COO & 运营总监', desc: '10年互联网运营经验，服务500+企业' },
  { id: 4, initial: '刘', name: '刘总', role: 'CMO & 市场总监', desc: '12年市场营销经验，品牌建设专家' }
]

const techArch = [
  { id: 1, icon: '🏗️', title: '微服务架构', desc: '采用微服务架构设计，模块化部署，支持弹性扩展，保障系统高可用性' },
  { id: 2, icon: '☁️', title: '云原生技术', desc: '基于Kubernetes容器编排，支持多云部署，实现资源动态调度和自动扩缩容' },
  { id: 3, icon: '🔐', title: '安全防护', desc: '多层安全防护体系，数据加密传输，访问权限控制，符合等保三级要求' }
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

/* 统计数据区域 */
.stats-section {
    padding: 100px 40px;
    background: linear-gradient(135deg, #F5F5F7 0%, #FFFFFF 100%);
}

.stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.stat-card {
    background: #FFFFFF;
    border-radius: 16px;
    padding: 40px;
    text-align: center;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
    transition: transform 0.3s, box-shadow 0.3s;
}

.stat-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
}

.stat-title {
    font-size: 16px;
    color: #1D4ED8;
    font-weight: 600;
    margin-bottom: 16px;
}

.stat-value {
    font-size: 48px;
    font-weight: 700;
    color: #1D1D1F;
    margin-bottom: 8px;
    line-height: 1.2;
}

.stat-desc {
    font-size: 14px;
    color: #6E6E73;
    line-height: 1.5;
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

/* 认证资质区域 */
.certifications-section {
    padding: 100px 40px;
    background: #FFFFFF;
}

.cert-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.cert-item {
    background: #F5F5F7;
    border-radius: 12px;
    padding: 30px 20px;
    text-align: center;
    transition: transform 0.3s, box-shadow 0.3s;
}

.cert-item:hover {
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
}

.cert-badge {
    width: 80px;
    height: 80px;
    background: linear-gradient(135deg, #1D4ED8 0%, #0066CC 100%);
    border-radius: 50%;
    margin: 0 auto 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 32px;
    font-weight: bold;
    color: #FFFFFF;
}

.cert-name {
    font-size: 16px;
    font-weight: 600;
    color: #1D1D1F;
    margin-bottom: 8px;
}

.cert-desc {
    font-size: 13px;
    color: #6E6E73;
}

/* 优势特色区域 */
.features-section {
    padding: 100px 40px;
    background: #F5F5F7;
}

.features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.feature-item {
    background: #FFFFFF;
    border-radius: 16px;
    padding: 40px;
    transition: transform 0.3s, box-shadow 0.3s;
}

.feature-item:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.feature-icon {
    font-size: 40px;
    margin-bottom: 20px;
}

.feature-item h3 {
    font-size: 22px;
    color: #1D1D1F;
    margin-bottom: 12px;
}

.feature-item p {
    font-size: 15px;
    color: #6E6E73;
    line-height: 1.6;
}

/* 客户案例区域 */
.clients-section {
    padding: 100px 40px;
    background: #FFFFFF;
}

.clients-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.client-logo {
    background: #F5F5F7;
    border-radius: 12px;
    padding: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 120px;
    transition: transform 0.3s, box-shadow 0.3s;
    font-size: 24px;
    font-weight: 600;
    color: #1D4ED8;
}

.client-logo:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}

/* 客户评价区域 */
.testimonials-section {
    padding: 100px 40px;
    background: #F5F5F7;
}

.testimonials-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.testimonial-card {
    background: #FFFFFF;
    border-radius: 16px;
    padding: 40px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
    transition: transform 0.3s, box-shadow 0.3s;
}

.testimonial-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
}

.testimonial-rating {
    color: #FFB800;
    font-size: 18px;
    margin-bottom: 16px;
}

.testimonial-content {
    font-size: 16px;
    color: #1D1D1F;
    line-height: 1.8;
    margin-bottom: 24px;
    font-style: italic;
}

.testimonial-author {
    display: flex;
    align-items: center;
    gap: 16px;
}

.author-avatar {
    width: 50px;
    height: 50px;
    background: linear-gradient(135deg, #1D4ED8 0%, #0066CC 100%);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #FFFFFF;
    font-weight: 600;
    font-size: 20px;
}

.author-info h4 {
    font-size: 16px;
    color: #1D1D1F;
    margin-bottom: 4px;
}

.author-info p {
    font-size: 14px;
    color: #6E6E73;
}

/* 服务流程区域 */
.process-section {
    padding: 100px 40px;
    background: #FFFFFF;
}

.process-steps {
    display: flex;
    justify-content: space-between;
    max-width: 1200px;
    margin: 0 auto;
    position: relative;
    padding: 0 20px;
}

.process-step {
    flex: 1;
    text-align: center;
    position: relative;
    z-index: 1;
}

.step-number {
    width: 60px;
    height: 60px;
    background: linear-gradient(135deg, #1D4ED8 0%, #0066CC 100%);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #FFFFFF;
    font-size: 24px;
    font-weight: 700;
    margin: 0 auto 20px;
    position: relative;
    z-index: 2;
}

.step-title {
    font-size: 18px;
    font-weight: 600;
    color: #1D1D1F;
    margin-bottom: 12px;
}

.step-desc {
    font-size: 14px;
    color: #6E6E73;
    line-height: 1.6;
}

.process-steps::before {
    content: '';
    position: absolute;
    top: 30px;
    left: 80px;
    right: 80px;
    height: 2px;
    background: #E5E5E7;
    z-index: 0;
}

/* 技术优势区域 */
.tech-section {
    padding: 100px 40px;
    background: linear-gradient(135deg, #F5F5F7 0%, #FFFFFF 100%);
}

.tech-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    max-width: 1200px;
    margin: 0 auto;
}

.tech-item {
    background: #FFFFFF;
    border-radius: 12px;
    padding: 24px;
    text-align: center;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
    transition: transform 0.3s, box-shadow 0.3s;
}

.tech-item:hover {
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
}

.tech-name {
    font-size: 16px;
    font-weight: 600;
    color: #1D1D1F;
}

/* 成功案例区域 */
.cases-section {
    padding: 100px 40px;
    background: #FFFFFF;
}

.cases-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.case-card {
    background: #F5F5F7;
    border-radius: 16px;
    overflow: hidden;
    transition: transform 0.3s, box-shadow 0.3s;
}

.case-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.case-image {
    width: 100%;
    height: 200px;
    background: linear-gradient(135deg, #1D4ED8 0%, #0066CC 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 48px;
    color: #FFFFFF;
}

.case-content {
    padding: 30px;
}

.case-tag {
    display: inline-block;
    background: #1D4ED8;
    color: #FFFFFF;
    padding: 4px 12px;
    border-radius: 12px;
    font-size: 12px;
    margin-bottom: 16px;
}

.case-title {
    font-size: 20px;
    font-weight: 600;
    color: #1D1D1F;
    margin-bottom: 12px;
}

.case-desc {
    font-size: 14px;
    color: #6E6E73;
    line-height: 1.6;
    margin-bottom: 16px;
}

.case-result {
    display: flex;
    gap: 20px;
    padding-top: 16px;
    border-top: 1px solid rgba(0, 0, 0, 0.1);
}

.result-item {
    flex: 1;
}

.result-value {
    font-size: 24px;
    font-weight: 700;
    color: #1D4ED8;
    margin-bottom: 4px;
}

.result-label {
    font-size: 12px;
    color: #6E6E73;
}

/* 新闻动态区域 */
.news-section {
    padding: 100px 40px;
    background: #F5F5F7;
}

.news-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.news-card {
    background: #FFFFFF;
    border-radius: 16px;
    overflow: hidden;
    transition: transform 0.3s, box-shadow 0.3s;
}

.news-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.news-date {
    background: #1D4ED8;
    color: #FFFFFF;
    padding: 8px 16px;
    font-size: 12px;
    font-weight: 600;
    display: inline-block;
    margin: 20px 20px 0;
    border-radius: 4px;
}

.news-content {
    padding: 20px;
}

.news-title {
    font-size: 18px;
    font-weight: 600;
    color: #1D1D1F;
    margin-bottom: 12px;
    line-height: 1.4;
}

.news-excerpt {
    font-size: 14px;
    color: #6E6E73;
    line-height: 1.6;
    margin-bottom: 16px;
}

.news-link {
    color: #1D4ED8;
    font-size: 14px;
    font-weight: 600;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 4px;
}

.news-link:hover {
    text-decoration: underline;
}

/* 行业解决方案区域 */
.industries-section {
    padding: 100px 40px;
    background: #FFFFFF;
}

.industries-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.industry-card {
    background: #F5F5F7;
    border-radius: 16px;
    padding: 40px;
    text-align: center;
    transition: transform 0.3s, box-shadow 0.3s;
}

.industry-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.industry-icon {
    font-size: 48px;
    margin-bottom: 20px;
}

.industry-name {
    font-size: 20px;
    font-weight: 600;
    color: #1D1D1F;
    margin-bottom: 12px;
}

.industry-desc {
    font-size: 14px;
    color: #6E6E73;
    line-height: 1.6;
}

/* 奖项荣誉区域 */
.awards-section {
    padding: 100px 40px;
    background: linear-gradient(135deg, #F5F5F7 0%, #FFFFFF 100%);
}

.awards-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.award-item {
    background: #FFFFFF;
    border-radius: 16px;
    padding: 30px 20px;
    text-align: center;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
    transition: transform 0.3s, box-shadow 0.3s;
}

.award-item:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
}

.award-icon {
    font-size: 40px;
    margin-bottom: 16px;
}

.award-name {
    font-size: 16px;
    font-weight: 600;
    color: #1D1D1F;
    margin-bottom: 8px;
}

.award-year {
    font-size: 14px;
    color: #6E6E73;
}

/* 团队介绍区域 */
.team-section {
    padding: 100px 40px;
    background: #FFFFFF;
}

.team-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.team-card {
    background: #F5F5F7;
    border-radius: 16px;
    padding: 40px;
    text-align: center;
    transition: transform 0.3s, box-shadow 0.3s;
}

.team-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.team-avatar {
    width: 100px;
    height: 100px;
    background: linear-gradient(135deg, #1D4ED8 0%, #0066CC 100%);
    border-radius: 50%;
    margin: 0 auto 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #FFFFFF;
    font-size: 40px;
    font-weight: bold;
}

.team-card h3 {
    font-size: 20px;
    color: #1D1D1F;
    margin-bottom: 8px;
}

.team-role {
    font-size: 14px;
    color: #6E6E73;
    margin-bottom: 12px;
}

.team-desc {
    font-size: 14px;
    color: #6E6E73;
    line-height: 1.6;
}

/* 技术架构区域 */
.tech-arch-section {
    padding: 100px 40px;
    background: #F5F5F7;
}

.tech-arch-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 30px;
    max-width: 1200px;
    margin: 0 auto;
}

.tech-arch-card {
    background: #FFFFFF;
    border-radius: 16px;
    padding: 40px;
    transition: transform 0.3s, box-shadow 0.3s;
}

.tech-arch-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.tech-arch-icon {
    font-size: 40px;
    margin-bottom: 20px;
}

.tech-arch-card h3 {
    font-size: 22px;
    color: #1D1D1F;
    margin-bottom: 16px;
}

.tech-arch-card p {
    font-size: 15px;
    color: #6E6E73;
    line-height: 1.6;
}

/* 加入我们区域 */
.joinus-section {
    padding: 100px 40px;
    background: linear-gradient(135deg, #1D4ED8 0%, #0066CC 100%);
    color: #FFFFFF;
    text-align: center;
}

.joinus-content h2 {
    font-size: 48px;
    font-weight: 700;
    margin-bottom: 24px;
    color: #FFFFFF;
}

.joinus-content p {
    font-size: 20px;
    margin-bottom: 40px;
    opacity: 0.9;
    max-width: 800px;
    margin-left: auto;
    margin-right: auto;
}

.joinus-button {
    display: inline-block;
    padding: 16px 40px;
    background: #FFFFFF;
    color: #1D4ED8;
    text-decoration: none;
    border-radius: 8px;
    font-size: 18px;
    font-weight: 600;
    transition: transform 0.3s, box-shadow 0.3s;
    cursor: pointer;
}

.joinus-button:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 30px rgba(255, 255, 255, 0.3);
}

@media (max-width: 768px) {
    /* Hero 区域优化 */
    .hero {
        padding: 60px 20px;
    }

    .hero h1 {
        font-size: 28px;
        margin-bottom: 12px;
    }

    .hero p {
        font-size: 16px;
        margin-bottom: 24px;
    }

    /* 区域 padding 优化 */
    .stats-section,
    .services,
    .certifications-section,
    .features-section,
    .clients-section,
    .testimonials-section,
    .process-section,
    .tech-section,
    .cases-section,
    .news-section,
    .industries-section,
    .awards-section,
    .team-section,
    .tech-arch-section,
    .joinus-section {
        padding: 40px 20px;
    }

    /* 标题优化 */
    .section-title {
        font-size: 32px;
        margin-bottom: 30px;
    }

    /* 统计数据区域 */
    .stats-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 16px;
    }

    .stat-card {
        padding: 24px 16px;
    }

    .stat-title {
        font-size: 14px;
        margin-bottom: 12px;
    }

    .stat-value {
        font-size: 28px;
        margin-bottom: 6px;
    }

    .stat-desc {
        font-size: 12px;
    }

    /* 服务卡片 */
    .services-grid {
        grid-template-columns: 1fr;
        gap: 16px;
    }

    .service-card {
        padding: 24px;
    }

    .service-icon {
        width: 60px;
        height: 60px;
        font-size: 24px;
        margin-bottom: 16px;
    }

    .service-card h3 {
        font-size: 20px;
        margin-bottom: 12px;
    }

    .service-card p {
        font-size: 14px;
    }

    /* 认证资质 */
    .cert-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 16px;
    }

    .cert-item {
        padding: 20px 12px;
    }

    .cert-badge {
        width: 60px;
        height: 60px;
        font-size: 24px;
        margin-bottom: 12px;
    }

    .cert-name {
        font-size: 14px;
        margin-bottom: 6px;
    }

    .cert-desc {
        font-size: 12px;
    }

    /* 优势特色 */
    .features-grid {
        grid-template-columns: 1fr;
        gap: 16px;
    }

    .feature-item {
        padding: 24px;
    }

    .feature-icon {
        font-size: 32px;
        margin-bottom: 16px;
    }

    .feature-item h3 {
        font-size: 18px;
        margin-bottom: 10px;
    }

    .feature-item p {
        font-size: 14px;
    }

    /* 客户案例 */
    .clients-grid {
        grid-template-columns: repeat(3, 1fr);
        gap: 12px;
    }

    .client-logo {
        padding: 20px 12px;
        height: 80px;
        font-size: 16px;
    }

    /* 客户评价 */
    .testimonials-grid {
        grid-template-columns: 1fr;
        gap: 16px;
    }

    .testimonial-card {
        padding: 24px;
    }

    .testimonial-rating {
        font-size: 16px;
        margin-bottom: 12px;
    }

    .testimonial-content {
        font-size: 14px;
        margin-bottom: 16px;
    }

    .author-avatar {
        width: 40px;
        height: 40px;
        font-size: 16px;
    }

    .author-info h4 {
        font-size: 14px;
    }

    .author-info p {
        font-size: 12px;
    }

    /* 服务流程 */
    .process-steps {
        flex-direction: column;
        gap: 24px;
        padding: 0 10px;
    }

    .process-steps::before {
        display: none;
    }

    .step-number {
        width: 50px;
        height: 50px;
        font-size: 20px;
        margin-bottom: 12px;
    }

    .step-title {
        font-size: 16px;
        margin-bottom: 8px;
    }

    .step-desc {
        font-size: 13px;
    }

    /* 技术优势 */
    .tech-list {
        grid-template-columns: repeat(2, 1fr);
        gap: 12px;
    }

    .tech-item {
        padding: 16px;
    }

    .tech-name {
        font-size: 14px;
    }

    /* 成功案例 */
    .cases-grid {
        grid-template-columns: 1fr;
        gap: 16px;
    }

    .case-image {
        height: 150px;
        font-size: 36px;
    }

    .case-content {
        padding: 20px;
    }

    .case-title {
        font-size: 18px;
        margin-bottom: 10px;
    }

    .case-desc {
        font-size: 13px;
        margin-bottom: 12px;
    }

    .result-value {
        font-size: 20px;
    }

    .result-label {
        font-size: 11px;
    }

    /* 新闻动态 */
    .news-grid {
        grid-template-columns: 1fr;
        gap: 16px;
    }

    .news-date {
        margin: 16px 16px 0;
        padding: 6px 12px;
        font-size: 11px;
    }

    .news-content {
        padding: 16px;
    }

    .news-title {
        font-size: 16px;
        margin-bottom: 10px;
    }

    .news-excerpt {
        font-size: 13px;
        margin-bottom: 12px;
    }

    /* 行业解决方案 */
    .industries-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 16px;
    }

    .industry-card {
        padding: 24px;
    }

    .industry-icon {
        font-size: 36px;
        margin-bottom: 16px;
    }

    .industry-name {
        font-size: 18px;
        margin-bottom: 10px;
    }

    .industry-desc {
        font-size: 13px;
    }

    /* 奖项荣誉 */
    .awards-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 16px;
    }

    .award-item {
        padding: 20px 16px;
    }

    .award-icon {
        font-size: 32px;
        margin-bottom: 12px;
    }

    .award-name {
        font-size: 14px;
        margin-bottom: 6px;
    }

    .award-year {
        font-size: 12px;
    }

    /* 团队介绍 */
    .team-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 16px;
    }

    .team-card {
        padding: 24px;
    }

    .team-avatar {
        width: 80px;
        height: 80px;
        font-size: 32px;
        margin-bottom: 16px;
    }

    .team-card h3 {
        font-size: 18px;
        margin-bottom: 6px;
    }

    .team-role {
        font-size: 13px;
        margin-bottom: 10px;
    }

    .team-desc {
        font-size: 12px;
    }

    /* 技术架构 */
    .tech-arch-grid {
        grid-template-columns: 1fr;
        gap: 16px;
    }

    .tech-arch-card {
        padding: 24px;
    }

    .tech-arch-icon {
        font-size: 32px;
        margin-bottom: 16px;
    }

    .tech-arch-card h3 {
        font-size: 18px;
        margin-bottom: 12px;
    }

    .tech-arch-card p {
        font-size: 14px;
    }

    /* 加入我们 */
    .joinus-content h2 {
        font-size: 28px;
        margin-bottom: 16px;
    }

    .joinus-content p {
        font-size: 16px;
        margin-bottom: 24px;
    }

    .joinus-button {
        padding: 12px 32px;
        font-size: 16px;
    }
}
</style>

