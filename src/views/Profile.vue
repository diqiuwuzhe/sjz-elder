<template>
  <div class="profile-page">
    <div class="user-info">
      <div class="avatar">
        <el-avatar :size="80" src="https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png" />
      </div>
      <h2>用户昵称</h2>
      <p class="user-id">ID: 888888</p>
    </div>

    <div class="menu-list">
      <div class="menu-group">
        <div class="menu-title">我的服务</div>
        <el-cell-group>
          <el-cell title="我的预约" :border="false">
            <template #icon>
              <el-icon class="menu-icon"><Calendar /></el-icon>
            </template>
            <template #default>
              <el-icon><ArrowRight /></el-icon>
            </template>
          </el-cell>
          <el-cell title="浏览历史" :border="false">
            <template #icon>
              <el-icon class="menu-icon"><Timer /></el-icon>
            </template>
            <template #default>
              <el-icon><ArrowRight /></el-icon>
            </template>
          </el-cell>
          <el-cell title="我的评价" :border="false">
            <template #icon>
              <el-icon class="menu-icon"><ChatDotRound /></el-icon>
            </template>
            <template #default>
              <el-icon><ArrowRight /></el-icon>
            </template>
          </el-cell>
        </el-cell-group>
      </div>

      <div class="menu-group">
        <div class="menu-title">系统设置</div>
        <el-cell-group>
          <el-cell title="消息通知" :border="false">
            <template #icon>
              <el-icon class="menu-icon"><Bell /></el-icon>
            </template>
            <template #default>
              <el-switch v-model="notifications" />
            </template>
          </el-cell>
          <el-cell title="隐私设置" :border="false">
            <template #icon>
              <el-icon class="menu-icon"><Lock /></el-icon>
            </template>
            <template #default>
              <el-icon><ArrowRight /></el-icon>
            </template>
          </el-cell>
          <el-cell title="关于我们" :border="false">
            <template #icon>
              <el-icon class="menu-icon"><InfoFilled /></el-icon>
            </template>
            <template #default>
              <el-icon><ArrowRight /></el-icon>
            </template>
          </el-cell>
        </el-cell-group>
      </div>
    </div>

    <el-button type="danger" plain class="logout-btn">退出登录</el-button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import {
  Calendar,
  Timer,
  ChatDotRound,
  Bell,
  Lock,
  InfoFilled,
  ArrowRight
} from '@element-plus/icons-vue'

const notifications = ref(true)
</script>

<style scoped>
.profile-page {
  min-height: 100vh;
  background: #f5f7fa;
  padding-bottom: 60px;
}

.user-info {
  background: #409EFF;
  color: #fff;
  padding: 30px 20px;
  text-align: center;
}

.avatar {
  margin-bottom: 15px;
}

.user-info h2 {
  margin: 0;
  font-size: 20px;
}

.user-id {
  margin: 5px 0 0;
  font-size: 14px;
  opacity: 0.8;
}

.menu-list {
  padding: 20px;
}

.menu-group {
  background: #fff;
  border-radius: 10px;
  margin-bottom: 20px;
  overflow: hidden;
}

.menu-title {
  padding: 15px;
  font-size: 16px;
  font-weight: bold;
  color: #333;
  border-bottom: 1px solid #eee;
}

.menu-icon {
  font-size: 20px;
  margin-right: 10px;
  color: #409EFF;
}

:deep(.el-cell) {
  padding: 15px;
}

:deep(.el-cell__title) {
  font-size: 16px;
}

.logout-btn {
  width: calc(100% - 40px);
  margin: 20px;
}
</style>