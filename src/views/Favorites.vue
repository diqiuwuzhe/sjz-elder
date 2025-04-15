<template>
  <div class="favorites-page">
    <div class="header">
      <h1>我的收藏</h1>
    </div>

    <div class="favorites-list" v-if="favorites.length > 0">
      <div v-for="item in favorites" :key="item.id" class="institution-card">
        <div class="card-tag" :class="item.type === '公办' ? 'public' : item.type === '医养结合' ? 'medical' : 'private'">{{ item.type }}</div>
        <h3>{{ item.name }}</h3>
        <div class="location">{{ item.district }}</div>
        <div class="info">
          <el-rate v-model="item.rating" disabled text-color="#ff9900" />
          <span class="distance">距离{{ item.distance }}km</span>
        </div>
        <div class="price">¥{{ item.price }}/月</div>
        <div class="action-buttons">
          <el-button type="primary" @click="$router.push(`/detail/${item.id}`)">查看详情</el-button>
          <el-button type="danger" plain @click="removeFavorite(item.id)">取消收藏</el-button>
        </div>
      </div>
    </div>

    <div class="empty-state" v-else>
      <el-empty description="暂无收藏的养老机构">
        <el-button type="primary" @click="$router.push('/list')">去发现机构</el-button>
      </el-empty>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const favorites = ref([
  {
    id: 1,
    name: '石家庄市老年公寓',
    district: '长安区',
    type: '公办',
    rating: 4.2,
    distance: 1.2,
    price: '1500-3000'
  },
  {
    id: 2,
    name: '康乐老年护理中心',
    district: '裕华区',
    type: '医养结合',
    rating: 4.8,
    distance: 2.5,
    price: '2500-4500'
  }
])

const removeFavorite = (id) => {
  favorites.value = favorites.value.filter(item => item.id !== id)
}
</script>

<style scoped>
.favorites-page {
  padding: 20px;
  padding-bottom: 80px;
}

.header {
  margin-bottom: 20px;
}

.header h1 {
  font-size: 24px;
  color: #409EFF;
  margin: 0;
}

.favorites-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.institution-card {
  background: #fff;
  border-radius: 10px;
  padding: 15px;
  position: relative;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
}

.card-tag {
  position: absolute;
  top: 10px;
  right: 10px;
  color: #fff;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 12px;
}

.card-tag.public {
  background: #67C23A;
}

.card-tag.medical {
  background: #409EFF;
}

.card-tag.private {
  background: #909399;
}

.institution-card h3 {
  margin: 0 0 8px;
  font-size: 16px;
}

.location {
  color: #909399;
  font-size: 14px;
  margin-bottom: 8px;
}

.info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8px;
}

.distance {
  color: #909399;
  font-size: 14px;
}

.price {
  color: #F56C6C;
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 10px;
}

.action-buttons {
  display: flex;
  gap: 10px;
}

.action-buttons .el-button {
  flex: 1;
}

.empty-state {
  margin-top: 100px;
}
</style>