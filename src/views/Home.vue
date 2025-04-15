<template>
  <div class="home">
    <div class="header">
      <h1>石家庄养老服务</h1>
      <div class="search-box">
        <el-input
          v-model="searchText"
          placeholder="搜索养老机构名称"
          :prefix-icon="Search"
        />
      </div>
    </div>

    <div class="feature-grid">
      <div class="feature-item" @click="$router.push('/list')">
        <el-icon class="icon"><HomeFilled /></el-icon>
        <span>机构查询</span>
      </div>
      <div class="feature-item" @click="$router.push('/list?sort=price')">
        <el-icon class="icon"><Discount /></el-icon>
        <span>价格优惠</span>
      </div>
      <div class="feature-item" @click="$router.push('/list?sort=rating')">
        <el-icon class="icon"><Star /></el-icon>
        <span>优质推荐</span>
      </div>
    </div>

    <div class="section">
      <div class="section-header">
        <h2>精选养老机构</h2>
        <el-link @click="$router.push('/list')">查看更多 ></el-link>
      </div>
      <div class="institution-list">
        <div class="institution-card" v-for="item in featuredInstitutions" :key="item.id" @click="$router.push(`/detail/${item.id}`)">
          <div class="card-tag" :class="item.type === '公办' ? 'public' : item.type === '公建民营' ? 'mixed' : 'private'">{{ item.type }}</div>
          <div class="status-tag" :class="item.operationStatus === '运营中' ? 'operating' : 'not-operating'">{{ item.operationStatus }}</div>
          <h3>{{ item.name }}</h3>
          <div class="location">{{ item.district }}</div>
          <div class="mode-tags">
            <el-tag v-for="mode in (Array.isArray(item.mode) ? item.mode : [item.mode])" :key="mode" size="small" effect="plain">{{ mode }}</el-tag>
          </div>
          <div class="info">
            <div class="rating">星级：{{ item.rating }}</div>
            <div class="beds" v-if="item.beds">床位：{{ item.beds }}</div>
          </div>
          <div class="price" v-if="item.price">¥{{ item.price }}+/月</div>
          <div class="price" v-else>价格待定</div>
          <el-button type="primary" class="contact-btn" @click.stop="makePhoneCall">一键通话</el-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { Search, HomeFilled, Discount, Star } from '@element-plus/icons-vue'
import { institutions } from '../data/institutions.js'

const searchText = ref('')

const featuredInstitutions = ref(institutions.filter(item => item.featured))

const makePhoneCall = () => {
  window.location.href = `tel:16630134340`
}
</script>

<style scoped>
.home {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

.header {
  text-align: center;
  margin-bottom: 20px;
}

.header h1 {
  color: #409EFF;
  font-size: 24px;
  margin-bottom: 15px;
}

.search-box {
  margin: 0 auto;
  max-width: 500px;
}

.feature-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 15px;
  margin: 20px 0;
}

@media screen and (max-width: 768px) {
  .feature-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .institution-list {
    gap: 10px;
  }

  .institution-card {
    padding: 12px;
  }

  .institution-card h3 {
    font-size: 14px;
  }

  .location, .distance {
    font-size: 12px;
  }

  .price {
    font-size: 14px;
  }
}

.feature-item {
  background: #fff;
  border-radius: 10px;
  padding: 20px;
  text-align: center;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: transform 0.2s;
}

.feature-item:hover {
  transform: translateY(-2px);
}

.feature-item .icon {
  font-size: 32px;
  color: #409EFF;
  margin-bottom: 10px;
}

.feature-item span {
  display: block;
  color: #333;
  font-size: 14px;
}

.section {
  margin-top: 30px;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
}

.section-header h2 {
  font-size: 18px;
  margin: 0;
}

.institution-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
  padding: 0;
}

.institution-card {
  background: #fff;
  border-radius: 10px;
  padding: 15px;
  position: relative;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  height: 100%;
  transition: transform 0.2s;
}

.institution-card:hover {
  transform: translateY(-2px);
}

.status-tag {
  position: absolute;
  top: 40px;
  left: 10px;
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

.card-tag {
  position: absolute;
  top: 10px;
  right: 10px;
  padding: 4px 8px;
  border-radius: 4px;
  color: #fff;
  font-size: 12px;
}

.card-tag.public {
  background: #409EFF;
}

.card-tag.mixed {
  background: #E6A23C;
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

.mode-tags {
  margin: 10px 0;
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
}

.info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 10px 0;
  color: #666;
  font-size: 14px;
}

.rating, .beds {
  display: flex;
  align-items: center;
  gap: 5px;
}

.price {
  font-size: 18px;
  color: #F56C6C;
  font-weight: bold;
  margin: 10px 0;
  text-align: center;
}

.contact-btn {
  width: 100%;
}
</style>