<template>
  <div :class="store.mobileOpenState ? 'right' : 'right hidden'">
    <!-- 移动端 Logo -->
    <div class="logo text-hidden" @click="store.mobileFuncState = !store.mobileFuncState">
      <span class="bg">{{ siteUrl[0] }}</span>
      <span class="sm">.{{ siteUrl[1] }}</span>
    </div>
    <!-- 功能区 -->
    <Func />
    <!-- 网站链接 -->
    <Link />
  </div>
</template>

<script setup>
import { mainStore } from "@/store";
import Func from "@/views/Func/index.vue";
import Link from "@/components/Links.vue";

const store = mainStore();

// 站点链接
const siteUrl = computed(() => {
  const url = import.meta.env.VITE_SITE_URL;
  if (!url) return "imsyy.top".split(".");
  // 判断协议前缀
  if (url.startsWith("http://") || url.startsWith("https://")) {
    const urlFormat = url.replace(/^(https?:\/\/)/, "");
    return urlFormat.split(".");
  }
  return url.split(".");
});
</script>

<style lang="scss" scoped>
.right {
  width: 50%;
  margin-left: 0.75rem;
  transition: all 0.3s;
  
  @media (max-width: 720px) {
    position: fixed;
    top: 0;
    right: 0;
    width: 66%;
    height: 100vh;
    margin: 0;
    padding: 20px;
    background: rgba(0, 0, 0, 0.5);
    backdrop-filter: blur(10px);
    z-index: 999;
    transform: translateX(0);
    
    &.hidden {
      transform: translateX(100%);
    }
  }
  
  .logo {
    display: none;
    
    @media (max-width: 720px) {
      display: block;
      text-align: center;
      padding: 15px 0;
    }
  }
}
</style>
