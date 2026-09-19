<template>
  <div class="layout">
    <!-- 头部导航栏容器，一行：logo + 菜单 -->
    <header class="header-wrap">
      <div class="logo">汾陇的博客</div>

      <el-menu
        :default-active="activeRoute"
        class="el-menu-demo"
        mode="horizontal"
        :ellipsis="false"
        router  
        @select="handleSelect"
      >
        <el-menu-item index="/">首页</el-menu-item>
        <el-menu-item index="/Article/:id">博客</el-menu-item>
          <el-menu-item index="/About">关于</el-menu-item>
      </el-menu>
    </header>

    <!-- 路由出口 -->
    <main class="main-content">
      <router-view />
    </main>

    <!-- 底部 -->
    <footer>
      <p>@2026 汾陇的博客. 使用Vue3构建</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import { useRoute } from 'vue-router'
const route = useRoute()
const activeRoute = ref(route.path)

// 菜单点击回调
const handleSelect = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}

//监听路由变化，自动高亮菜单
watch(
  () => route.path,
  (newPath) => {
    activeRoute.value = newPath
  },
  { immediate: true }
)
</script>

<style scoped>
.layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
.header-wrap {
  display: flex;
  align-items: center;
  padding: 0 24px;
  border-bottom: 1px solid #e5e7eb;
}
.logo {
  font-size: 22px;
  font-weight: bold;
  color: #303133;
  margin-right: 32px;
}
.main-content {
  flex: 1;
  padding: 24px;
}
footer {
  text-align: center;
  padding: 16px;
  color: #666;
  font-size:14px;
}
/* 菜单样式穿透 */
:deep(.el-menu-demo) {
  border-bottom: none;
  flex:1;
}
</style>
