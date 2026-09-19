<template>
  <article class="article-detail" v-if="article">
    <h2>{{ article.title }}</h2>
    <p class="meta">文章编号：{{ article.id }}｜发布时间：{{ article.createTime }}</p>
    <div class="content">{{ article.content }}</div>
  </article>

  <!-- 加载中 -->
  <div v-else-if="loading" class="tip">加载文章中...</div>
  <!-- 找不到文章 -->
  <div v-else class="tip">该文章不存在</div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

interface Article {
  id: string
  title: string
  createTime: string
  content: string
}

const article = ref<Article | null>(null)
const loading = ref(false)

// 获取文章
const fetchArticle = async (id: string) => {
  loading.value = true
  article.value = null
  try {
    // 模拟接口，后续替换成 axios 请求
    article.value = {
      id,
      title: '第一版博客-最小可行性产品实践',
      createTime: '2026-09-19',
      content: '使用最小可行性产品发布博客页面，快速跑通核心流程。时间就是金钱，效率就是生命。',
    }
  } catch (err) {
    article.value = null
    console.error('获取文章失败：', err)
  } finally {
    loading.value = false
  }
}

// 监听路由id变化，切换文章
watch(
  () => route.params.id,
  (rawId) => {
    // 校验：必须是字符串，非空才请求
    if (typeof rawId === 'string' && rawId.trim()) {
      fetchArticle(rawId.trim())
    } else {
      article.value = null
    }
  },
  { immediate: true }
)
</script>

<style scoped>
.article-detail {
  max-width: 800px;
  margin: 0 auto;
  padding: 24px;
}
.meta {
  color: #666;
  font-size: 14px;
}
.content {
  margin-top: 16px;
  line-height: 1.8;
  font-size: 16px;
}
.tip {
  text-align: center;
  padding: 40px;
  color: #666;
}
</style>
