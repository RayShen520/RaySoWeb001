<template>
  <div class="contact-page">
    <section class="contact-section">
      <h2 class="section-title">联系我们</h2>
      <div class="contact-container">
        <form 
          class="contact-form" 
          name="contact" 
          netlify 
          netlify-honeypot="bot-field"
          data-netlify="true"
          @submit.prevent="handleSubmit"
        >
          <!-- Netlify 隐藏字段，用于防止垃圾邮件 -->
          <input type="hidden" name="form-name" value="contact" />
          <p style="display: none;">
            <label>Don't fill this out if you're human: <input name="bot-field" /></label>
          </p>
          <div class="form-group">
            <label for="wechat">微信号 <span class="optional">(选填)</span></label>
            <input 
              type="text" 
              id="wechat" 
              name="wechat"
              v-model="form.wechat"
              placeholder="请输入您的微信号"
            >
          </div>
          <div class="form-group">
            <label for="phone">手机号 <span class="optional">(选填)</span></label>
            <input 
              type="tel" 
              id="phone" 
              name="phone"
              v-model="form.phone"
              placeholder="请输入您的手机号"
            >
            <div class="form-note">请至少填写微信号或手机号其中一个</div>
          </div>
          <div class="form-group">
            <label for="message">咨询内容 <span class="optional">(选填)</span></label>
            <textarea 
              id="message" 
              name="message"
              v-model="form.message"
              placeholder="请描述您的咨询内容..."
            ></textarea>
          </div>
          <button 
            type="submit" 
            class="submit-btn" 
            :disabled="isSubmitting"
          >
            {{ isSubmitting ? '提交中...' : '提交咨询' }}
          </button>
        </form>

        <div class="contact-info">
          <h3>其他联系方式</h3>
          <p>我们会在收到您的咨询后尽快与您联系</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { inject } from 'vue'

const showToast = inject('showToast')

const form = ref({
  wechat: '',
  phone: '',
  message: ''
})

const isSubmitting = ref(false)

const handleSubmit = async (e) => {
  e.preventDefault()
  
  const { wechat, phone, message } = form.value

  // 验证至少填写一个联系方式
  if (!wechat.trim() && !phone.trim()) {
    showToast('请至少填写微信号或手机号')
    return
  }

  // 验证手机号格式（如果填写了）
  if (phone.trim() && !/^1[3-9]\d{9}$/.test(phone.trim())) {
    showToast('请输入正确的手机号格式')
    return
  }

  // 禁用提交按钮
  isSubmitting.value = true

  // 使用 Netlify Forms 提交
  try {
    // 构建表单数据，确保包含 form-name
    const formData = new URLSearchParams()
    formData.append('form-name', 'contact')
    formData.append('wechat', wechat.trim())
    formData.append('phone', phone.trim())
    formData.append('message', message.trim())
    
    const response = await fetch('/', {
      method: 'POST',
      headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
      body: formData.toString()
    })

    if (response.ok) {
      showToast('提交成功！我们会尽快与您联系。')
      form.value = {
        wechat: '',
        phone: '',
        message: ''
      }
    } else {
      console.error('Form submission error:', response.status, response.statusText)
      showToast('提交失败，请稍后重试。')
    }
  } catch (error) {
    console.error('Form submission error:', error)
    showToast('提交失败，请稍后重试。')
  } finally {
    isSubmitting.value = false
  }
}
</script>

<style scoped>
.contact-page {
    min-height: calc(100vh - 80px);
    margin-top: 80px;
}

.contact-section {
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

.contact-container {
    max-width: 800px;
    margin: 0 auto;
}

.contact-form {
    background: #F5F5F7;
    padding: 40px;
    border-radius: 16px;
}

.form-group {
    margin-bottom: 24px;
}

.form-group label {
    display: block;
    margin-bottom: 8px;
    color: #1D1D1F;
    font-weight: 500;
}

.optional {
    color: #6E6E73;
    font-weight: normal;
}

.form-group input,
.form-group textarea {
    width: 100%;
    padding: 14px 16px;
    border: 2px solid rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    font-size: 16px;
    font-family: inherit;
    transition: border-color 0.3s;
    background: #FFFFFF;
}

.form-group input:focus,
.form-group textarea:focus {
    outline: none;
    border-color: #1D4ED8;
}

.form-group textarea {
    resize: vertical;
    min-height: 120px;
}

.form-note {
    font-size: 14px;
    color: #6E6E73;
    margin-top: 4px;
}

.submit-btn {
    width: 100%;
    padding: 16px;
    background: #1D4ED8;
    color: #FFFFFF;
    border: none;
    border-radius: 8px;
    font-size: 18px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.3s;
}

.submit-btn:hover:not(:disabled) {
    background: #1E40AF;
}

.submit-btn:disabled {
    background: #CCCCCC;
    cursor: not-allowed;
}

.contact-info {
    margin-top: 60px;
    text-align: center;
}

.contact-info h3 {
    font-size: 24px;
    color: #1D1D1F;
    margin-bottom: 20px;
}

.contact-info p {
    font-size: 16px;
    color: #6E6E73;
    margin-bottom: 8px;
}

@media (max-width: 768px) {
    /* 区域 padding 优化 */
    .contact-section {
        padding: 40px 20px;
    }

    /* 标题优化 */
    .section-title {
        font-size: 32px;
        margin-bottom: 30px;
    }

    .contact-form {
        padding: 24px;
    }

    .form-group {
        margin-bottom: 20px;
    }

    .form-group label {
        font-size: 14px;
        margin-bottom: 6px;
    }

    .form-group input,
    .form-group textarea {
        padding: 12px 14px;
        font-size: 14px;
    }

    .form-group textarea {
        min-height: 100px;
    }

    .form-note {
        font-size: 12px;
    }

    .submit-btn {
        padding: 14px;
        font-size: 16px;
    }

    .contact-info {
        margin-top: 40px;
    }

    .contact-info h3 {
        font-size: 20px;
        margin-bottom: 16px;
    }

    .contact-info p {
        font-size: 14px;
    }
}
</style>

