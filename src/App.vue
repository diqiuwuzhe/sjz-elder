<template>
  <div class="app-container">
    <SocialLinks />
    <router-view></router-view>
    <div class="bottom-nav">
      <router-link to="/" class="nav-item">
        <el-icon><HomeFilled /></el-icon>
        <span>首页</span>
      </router-link>
      <router-link to="/list" class="nav-item">
        <el-icon><List /></el-icon>
        <span>机构列表</span>
      </router-link>
      <router-link to="/favorites" class="nav-item">
        <el-icon><Star /></el-icon>
        <span>我的收藏</span>
      </router-link>
      <router-link to="/profile" class="nav-item">
        <el-icon><User /></el-icon>
        <span>个人中心</span>
      </router-link>
    </div>
  </div>
</template>

<script setup>
import { HomeFilled, List, Star, User } from '@element-plus/icons-vue'
import SocialLinks from './components/SocialLinks.vue'
</script>

<style scoped>
.app-container {
  min-height: 100vh;
  padding-bottom: 60px;
  box-sizing: border-box;
}

.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 60px;
  background: #fff;
  display: flex;
  justify-content: space-around;
  align-items: center;
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #666;
  text-decoration: none;
  font-size: 12px;
}

.nav-item .el-icon {
  font-size: 24px;
  margin-bottom: 2px;
}

.nav-item.router-link-active {
  color: #409EFF;
}
</style>