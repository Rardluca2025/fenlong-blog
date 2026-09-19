<!-- 展示文章列表 -->
 <script setup lang="ts">  
 import { ref } from 'vue'

 //模拟博客数据
 const posts = ref([
    { id:1, title:'博客的最小可行产品上线', summary:'最低成本、最短时间交付可用版本', date:'2026-09-19' }
 ])
 </script>

 <template>
  <div class="home">
    <h2>文章列表</h2>
    <ul>
      <li v-for="post in posts" :key="post.id" class="post-item">
        <!-- 跳转到详细页 -->
        <router-link :to="`/article/${post.id}`">
          <h3>{{ post.title }}</h3>
        </router-link>
            <p>{{ post.summary }}</p>
           <p class="post-date">{{ post.date }}</p>
    
     
      </li>
    </ul>
  </div>
      <!-- 技术栈板块 -->
     <div>
      <h3 class="section-title">技术栈</h3>
       <div class="badge-container"></div>
      <span class="badge-item" style="--brand-color: #e34f26">
        <img
          src="https://img.shields.io/badge/HTML5-181717?style=for-the-badge&logo=html5&logoColor=e34f26"
          alt="HTML5"
        />
      </span>
      <span class="badge-item" style="--brand-color: #663399">
        <img
          src="https://img.shields.io/badge/CSS-181717?style=for-the-badge&logo=css&logoColor=663399"
          alt="CSS"
        />
      </span>
      <span class="badge-item" style="--brand-color: #f7df1e">
        <img
          src="https://img.shields.io/badge/JavaScript-181717?style=for-the-badge&logo=javascript&logoColor=f7df1e"
          alt="JavaScript"
        />
      </span>
      <span class="badge-item" style="--brand-color: #4fc08d">
        <img
          src="https://img.shields.io/badge/Vue.js-181717?style=for-the-badge&logo=vuedotjs&logoColor=4fc08d"
          alt="Vue.js"
        />
      </span>
 
    </div>

<!-- 学习工具板块 -->

      <h3 class="section-title">学习工具</h3>
          <div class="badge-container">
   <span class="badge-item" style="--brand-color: #04AA6D;">
      <img src="https://img.shields.io/badge/W3_Schools-181717?style=for-the-badge&logo=w3schools&logoColor=04AA6D" alt="W3 Schools">
    </span>
    <span class="badge-item" style="--brand-color: #ffffff;">
      <img src="https://img.shields.io/badge/MDN_Web_Docs-181717?style=for-the-badge&logo=mdnwebdocs&logoColor=ffffff" alt="MDN Web Docs">
    </span>
    </div>
 </template>