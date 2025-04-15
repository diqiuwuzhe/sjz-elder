<template>
  <div class="detail-page">
    <div class="institution-info">
      <div class="header">
        <h2>{{ institution.name }}</h2>
        <div class="status-tag" :class="institution.operationStatus === '运营中' ? 'operating' : 'not-operating'">{{ institution.operationStatus }}</div>
        <div class="tag" :class="institution.type === '公办' ? 'public' : institution.type === '公建民营' ? 'mixed' : 'private'">{{ institution.type }}</div>
      </div>

      <div class="mode-info">
        <el-tag v-for="mode in (Array.isArray(institution.mode) ? institution.mode : [institution.mode])" :key="mode" size="small" effect="plain">{{ mode }}</el-tag>
      </div>

      <div class="rating-info">
        <span class="rating">星级：{{ institution.rating }}</span>
      </div>

      <div class="basic-info">
        <div class="info-item">
          <span class="label">所在区域</span>
          <span class="value">{{ institution.district }}</span>
        </div>
        <div class="info-item">
          <span class="label">床位数量</span>
          <span class="value">{{ institution.beds || '暂无信息' }}</span>
        </div>
        <div class="info-item">
          <span class="label">机构性质</span>
          <span class="value">{{ institution.type }}</span>
        </div>
        <div class="info-item">
          <span class="label">月费用</span>
          <span class="value price">{{ institution.price ? `¥${institution.price}+/月` : '价格待定' }}</span>
        </div>
      </div>

      <div class="room-types" v-if="institution.roomTypes && institution.roomTypes.length > 0">
        <h3>房型信息</h3>
        <div class="room-tags">
          <el-tag v-for="type in institution.roomTypes" :key="type" size="small" effect="light">{{ type }}</el-tag>
        </div>
      </div>

      <div class="services" v-if="institution.services && institution.services.length > 0">
        <h3>特色服务</h3>
        <div class="service-tags">
          <el-tag v-for="service in institution.services" :key="service" size="small" type="success" effect="light">{{ service }}</el-tag>
        </div>
      </div>

      <el-button type="primary" class="contact-btn" @click="makePhoneCall">一键通话</el-button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import { institutions } from '../data/institutions.js'

const route = useRoute()
const institution = ref({})

const makePhoneCall = () => {
  window.location.href = `tel:16630134340`
}

onMounted(() => {
  const id = parseInt(route.params.id)
  const found = institutions.find(item => item.id === id)
  if (found) {
    institution.value = found
  }
})
</script>

<style scoped>
.detail-page {
  padding: 20px;
  max-width: 800px;
  margin: 0 auto;
}

.institution-info {
  background: #fff;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
  position: relative;
  padding-right: 100px;
}

.header h2 {
  margin: 0;
  font-size: 24px;
  font-weight: bold;
}

.status-tag {
  position: absolute;
  right: 100px;
  top: 0;
  padding: 4px 8px;
  border-radius: 4px;
  color: #fff;
  font-size: 12px;
}

.status-tag.operating {
  background: #67C23A;
}

.status-tag.not-operating {
  background: #909399;
}

.tag {
  position: absolute;
  right: 0;
  top: 0;
  color: #fff;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 12px;
}

.tag.public {
  background: #409EFF;
}

.tag.mixed {
  background: #E6A23C;
}

.tag.private {
  background: #909399;
}

.mode-info {
  margin: 15px 0;
  display: flex;
  gap: 10px;
}

.rating-info {
  margin: 15px 0;
  font-size: 16px;
  color: #E6A23C;
  font-weight: bold;
}

.basic-info {
  background: #f5f7fa;
  border-radius: 8px;
  padding: 20px;
  margin: 20px 0;
}

.info-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
  font-size: 14px;
}

.info-item:last-child {
  margin-bottom: 0;
}

.label {
  color: #909399;
}

.value {
  color: #303133;
}

.value.price {
  color: #F56C6C;
  font-weight: bold;
  font-size: 16px;
}

.room-types,
.services {
  margin: 20px 0;
}

.room-types h3,
.services h3 {
  font-size: 16px;
  margin-bottom: 15px;
  color: #303133;
}

.room-tags,
.service-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.contact-btn {
  width: 100%;
  height: 44px;
  font-size: 16px;
  margin-top: 20px;
}
</style>