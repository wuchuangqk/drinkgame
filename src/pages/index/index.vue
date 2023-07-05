<template>
  <view class="page-full test">
    <navigator url="/pages/spin-bottle/spin-bottle">
      <button type="primary">转瓶子</button>
    </navigator>
    <navigator url="/pages/danmu/danmu">
      <button type="primary">手持弹幕</button>
    </navigator>
    <view class="test"></view>
  </view>
</template>

<script setup lang="ts">
</script>

<style scoped lang="scss">
.test {
  width: 200rpx;
  height: 200rpx;
  background-image: -webkit-linear-gradient(-180deg, rgba(255, 0, 255, 0.8) 10%, #f00 80%);
  // padding-top: 200rpx;
  // margin-top: -200rpx;
}
</style>
