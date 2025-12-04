<template>
  <div class="toast" v-if="message">
    {{ message }}
  </div>
</template>

<script setup>
defineProps({
  message: {
    type: String,
    default: ''
  }
})

defineEmits(['close'])
</script>

<style scoped>
.toast {
    position: fixed;
    bottom: 30px;
    right: 30px;
    background: #1D4ED8;
    color: #FFFFFF;
    padding: 16px 24px;
    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
    z-index: 2000;
    animation: slideIn 0.3s ease-out;
}

@keyframes slideIn {
    from {
        transform: translateX(100%);
        opacity: 0;
    }
    to {
        transform: translateX(0);
        opacity: 1;
    }
}
</style>

