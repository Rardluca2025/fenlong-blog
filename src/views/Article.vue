<template>
  <article class="article-detail" v-if="article">
    <h2>文章编号：{{ article.id }}</h2>
    <p class="meta">发布时间：{{ article.createTime }}</p>
    <div class="content">{{ article.content }}</div>
  </article>

  <!-- 加载中 -->
  <div v-else-if="loading">加载文章中...</div>
  <!-- 找不到文章 -->
  <div v-else>该文章不存在</div>
</template>

<script setup lang="ts">
import { ref, watch, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const articleId = ref<string>('')

interface Article {
  id: string
  title: string
  createTime: string
  content: string
}

const article = ref<Article | null>(null)
const loading = ref(false)

// 模拟从数据库/后端api获取文章
const fetchArticle = async (id: string) => {
  loading.value = true
  try {
    // 替换成真实axios/fetch请求
    // const res = await api.getArticle(id)
    // article.value = res.data
    article.value = {
      id:'0',
      title: '第一版博客-最小可行性产品实践',
      createTime: '2026-09-19',
      content: '使用最小可行性产品发布博客页面，快速跑通核心流程。时间就是金钱，效率就是生命。',
    }
  } catch (err) {
    article.value = null
    console.error('获取文章失败', err)
  } finally {
    loading.value = false
  }
}

// 监听路由参数变化：切换不同文章时重新请求
watch(
  () => route.params.id,
  (newId) => {
    if (typeof newId === 'string') {
      articleId.value = newId
      fetchArticle(newId)
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
}
</style>
