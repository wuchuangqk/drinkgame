<template>
  <view class="mask">
    <view class="dialog">
      <view class="title flex center">{{ title }}</view>
      <slot></slot>
    </view>
  </view>
</template>

<script setup lang="ts">
defineProps<{
  title: string
}>()
</script>

<style lang="scss" scope>
.mask {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
}

.dialog {
  width: 650rpx;
  height: 754rpx;
  background: url("/static/bg_tc@2x.png") no-repeat;
  background-size: cover;
  padding: 50rpx 50rpx 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.title {
  font-size: 36rpx;
  color: #FFFFFF;
  width: 312rpx;
  height: 61rpx;
  background: #F68B39;
  border: 3px solid #000000;
  border-radius: 31rpx;
}
</style>