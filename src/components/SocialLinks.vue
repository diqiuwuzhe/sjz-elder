<template>
  <div class="social-links">
    <el-popover
      placement="bottom"
      :width="200"
      trigger="hover"
      popper-class="qr-popover"
    >
      <template #reference>
        <div class="social-icon">
          <img src="/images/video-account.svg" alt="视频号" />
          <span>视频号</span>
        </div>
      </template>
      <div class="qr-code">
        <img src="/images/video-account-qr.png" alt="视频号二维码" />
        <p>扫码关注视频号</p>
      </div>
    </el-popover>

    <a
      href="https://www.douyin.com/user/MS4wLjABAAAAO4mNL7ZBNhO4Uut74IBegsDGgDQieEIZ3J5NWyb2kPnRitwWfCE6XGPjYJNcC4hv?from_tab_name=main"
      target="_blank"
      class="social-icon"
    >
      <img src="/images/douyin.svg" alt="抖音" />
      <span>抖音</span>
    </a>

    <a
      href="https://www.xiaohongshu.com/user/profile/66176b9e0000000003030a3e"
      target="_blank"
      class="social-icon"
    >
      <img src="/images/xiaohongshu.svg" alt="小红书" />
      <span>小红书</span>
    </a>
  </div>
</template>

<style scoped>
.social-links {
  position: fixed;
  top: 20px;
  right: 20px;
  display: flex;
  gap: 15px;
  z-index: 100;
}

.social-icon {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
  text-decoration: none;
  color: #333;
  transition: transform 0.3s ease;
}

.social-icon:hover {
  transform: scale(1.1) translateY(-5px);
}

.social-icon img {
  width: 24px;
  height: 24px;
  margin-bottom: 4px;
}

.social-icon span {
  font-size: 12px;
}

.qr-code {
  text-align: center;
}

.qr-code img {
  width: 160px;
  height: 160px;
  margin-bottom: 10px;
}

.qr-code p {
  margin: 0;
  font-size: 14px;
  color: #666;
}

:deep(.qr-popover) {
  padding: 15px;
}
</style>