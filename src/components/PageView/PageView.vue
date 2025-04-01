<script setup lang="ts">
const props = defineProps({
  headerBgColor: {
    type: String,
  },
});
</script>
<template>
  <div class="h-100vh flex flex-col">
    <div
      class="header min-h-10"
      :style="{
        backgroundColor: props.headerBgColor || 'white',
        boxShadow: `0 40px 0 0 ${props.headerBgColor}`,
      }">
      头部信息
    </div>
    <slot class="flex-1"></slot>
    <div class="footer">
      <div class="h-40px">tabbar</div>
    </div>
  </div>
</template>
<style scoped>
.header {
  padding-top: env(safe-area-inset-top);
}
.footer {
  padding-bottom: env(safe-area-inset-bottom);
  background: rgba(255, 255, 255, 0.3); /* 半透明背景 */
  backdrop-filter: blur(10px); /* 关键：背景模糊 */
  -webkit-backdrop-filter: blur(10px); /* Safari 兼容 */
  border-radius: 10px;
}
</style>
