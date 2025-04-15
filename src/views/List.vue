<template>
  <div class="list-page">
    <div class="filter-tabs">
      <div class="filter-row">
        <el-select v-model="activeOperationStatus" placeholder="运营状态" class="filter-select">
          <el-option label="全部状态" value="all" />
          <el-option label="运营中" value="运营中" />
          <el-option label="未运营" value="未运营" />
        </el-select>

        <el-select v-model="activeArea" placeholder="选择区域" class="filter-select">
          <el-option label="全部区域" value="all" />
          <el-option label="长安区" value="长安区" />
          <el-option label="新华区" value="新华区" />
          <el-option label="桥西区" value="桥西区" />
          <el-option label="裕华区" value="裕华区" />
          <el-option label="藁城区" value="藁城区" />
          <el-option label="鹿泉区" value="鹿泉区" />
          <el-option label="正定县" value="正定县" />
          <el-option label="栾城区" value="栾城区" />
        </el-select>

        <el-select v-model="activeMode" placeholder="选择模式" class="filter-select">
          <el-option label="全部模式" value="all" />
          <el-option label="居家" value="居家" />
          <el-option label="社区" value="社区" />
          <el-option label="机构" value="机构" />
          <el-option label="机构CCRC" value="机构CCRC" />
        </el-select>

        <el-select v-model="activeRating" placeholder="选择星级" class="filter-select">
          <el-option label="全部星级" value="all" />
          <el-option label="五级" value="5" />
          <el-option label="四级" value="4" />
          <el-option label="三级" value="3" />
          <el-option label="二级" value="2" />
          <el-option label="一级" value="1" />
          <el-option label="暂无" value="0" />
        </el-select>

        <el-select v-model="activeService" placeholder="特殊服务" class="filter-select">
          <el-option label="全部服务" value="all" />
          <el-option label="认知照护" value="认知照护" />
          <el-option label="日间照料" value="日间照料" />
          <el-option label="室内有摄像头" value="室内有摄像头" />
          <el-option label="医养结合（至少有社区医院）" value="医养结合（至少有社区医院）" />
          <el-option label="长期护理保险（长护险）" value="长期护理保险（长护险）" />
          <el-option label="中医药膳" value="中医药膳" />
          <el-option label="民族餐" value="民族餐" />
          <el-option label="助餐" value="助餐" />
          <el-option label="助娱" value="助娱" />
          <el-option label="助浴" value="助浴" />
        </el-select>

        <el-select v-model="activePriceRange" placeholder="价格范围" class="filter-select">
          <el-option label="全部价格" value="all" />
          <el-option label="1000+" value="1000" />
          <el-option label="2000+" value="2000" />
          <el-option label="3000+" value="3000" />
          <el-option label="4000+" value="4000" />
          <el-option label="5000+" value="5000" />
        </el-select>
      </div>
    </div>

    <div class="institution-list">
      <div v-for="item in filteredInstitutions" :key="item.id" class="institution-card" @click="handleCardClick(item)">
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
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'
import { institutions as institutionsData } from '../data/institutions.js'

const router = useRouter()

const makePhoneCall = () => {
  window.location.href = `tel:16630134340`
}

const activeArea = ref('all')
const activeMode = ref('all')
const activeRating = ref('all')
const activePriceRange = ref('all')
const sortType = ref('smart')
const activeOperationStatus = ref('all')
const activeService = ref('all')

const institutions = ref(institutionsData)

const filteredInstitutions = computed(() => {
  let result = [...institutions.value]
  
  // 区域筛选
  if (activeArea.value !== 'all') {
    result = result.filter(item => item.district === activeArea.value)
  }

  // 模式筛选
  if (activeMode.value !== 'all') {
    result = result.filter(item => {
      if (Array.isArray(item.mode)) {
        return item.mode.includes(activeMode.value)
      }
      return item.mode === activeMode.value
    })
  }

  // 运营状态筛选
  if (activeOperationStatus.value !== 'all') {
    result = result.filter(item => item.operationStatus === activeOperationStatus.value)
  }

  // 星级筛选
  if (activeRating.value !== 'all') {
    const ratingMap = {
      '5': '五级',
      '4': '四级',
      '3': '三级',
      '2': '二级',
      '1': '一级',
      '0': '暂无'
    }
    result = result.filter(item => item.rating === ratingMap[activeRating.value])
  }

  // 价格范围筛选
  if (activePriceRange.value !== 'all') {
    const minPrice = parseInt(activePriceRange.value)
    result = result.filter(item => item.price && item.price >= minPrice)
  }

  // 特殊服务筛选
  if (activeService.value !== 'all') {
    result = result.filter(item => item.services && item.services.includes(activeService.value))
  }

  // 排序
  if (sortType.value === 'price') {
    result.sort((a, b) => (a.price || 0) - (b.price || 0))
  } else if (sortType.value === 'special') {
    result.sort((a, b) => {
      const getScore = (item) => {
        let score = 0
        // 特殊服务加分
        if (item.services && Array.isArray(item.services)) {
          if (item.services.includes('医养结合')) score += 3
          if (item.services.includes('认知照护')) score += 2
          if (item.services.includes('长期护理保险')) score += 2
        }
        // 运营状态加分
        if (item.operationStatus === '运营中') score += 1
        if (item.price && item.price <= 3000) score += 2
        // 床位数量加分
        if (item.beds === '500+') score += 2
        // 特色服务加分
        if (item.services && item.services.length > 0) score += item.services.length
        // 星级加分
        const ratingScore = {
          '五级': 5,
          '四级': 4,
          '三级': 3,
          '二级': 2,
          '一级': 1,
          '暂无': 0
        }
        score += ratingScore[item.rating] || 0
        return score
      }
      return getScore(b) - getScore(a)
    })
  }
  return result
})

const handleCardClick = (item) => {
  router.push(`/detail/${item.id}`)
}
</script>

<style scoped>
.list-page {
  padding: 0 0 60px;
  max-width: 1200px;
  margin: 0 auto;
}

.filter-tabs {
  position: sticky;
  top: 0;
  background: #fff;
  z-index: 10;
  padding: 15px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.filter-row {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  max-width: 1200px;
  margin: 0 auto;
}

.filter-select {
  flex: 1;
  min-width: 150px;
}

.institution-list {
  padding: 20px;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
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

:deep(.el-tabs__nav) {
  width: 100%;
  display: flex;
}

:deep(.el-tabs__item) {
  flex: 1;
  text-align: center;
}

:deep(.el-radio-group) {
  display: flex;
  width: 100%;
}

:deep(.el-radio-button) {
  flex: 1;
}

:deep(.el-radio-button__inner) {
  width: 100%;
}
</style>