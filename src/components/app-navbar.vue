<template>
  <view>
    <view :style="{ height: statusBarHeight }"></view>
    <view class="title-text" @click="back">
      <text class="arrow">左</text>
      <text>返回</text>
    </view>
  </view>
</template>

<script setup lang="ts">
const statusBarHeight = uni.getSystemInfoSync().statusBarHeight + 'px'
const back = () => {
  uni.navigateBack()
}
</script>

<style lang="scss" scope>

.title-text {
  display: flex;
  align-items: center;
  color: #fff;
  font-size: 32rpx;
  height: 44px;
}

.arrow {
  margin: 0 28rpx 0 32rpx;
}
</style>