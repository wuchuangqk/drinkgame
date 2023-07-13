<template>
  <view class="page">
    <view :style="{ height: statusBarHeight }"></view>
    <view class="title-text"><text>酒桌游戏俱乐部</text></view>
    <view class="v1">
      <view class="v2 flex items-center hot" @click="nav('/pages/dice/dice')">
        <view class="flex-1">
          <view class="v3">疯狂摇骰子</view>
          <view class="v4">什么魂淡游戏下酒这么快！！</view>
        </view>
        <image src="http://admin.jlwp.vip/jjsq/ico_touzi@2x.png" style="width: 167rpx;height: 159rpx;" />
      </view>
      <view class="v2 flex items-center">
        <view class="flex-1">
          <view class="v3">鳄鱼拔牙</view>
          <view class="v4">都说鳄鱼口里拔牙最危险？</view>
        </view>
        <image src="http://admin.jlwp.vip/jjsq/icon_eyuby@2x.jpg" style="width: 184rpx;height: 159rpx;" />
      </view>
      <view class="v2 flex items-center" @click="nav('/pages/spin-bottle/spin-bottle')">
        <view class="flex-1">
          <view class="v3">转瓶子</view>
          <view class="v4">你怎么下酒这么快？</view>
        </view>
        <image src="http://admin.jlwp.vip/jjsq/icon_zpz@2x.jpg" style="width: 159rpx;height: 166rpx;" />
      </view>
      <view class="v2 flex items-center" @click="nav('/pages/bomb/bomb')">
        <view class="flex-1">
          <view class="v3">数字炸弹</view>
          <view class="v4">谁猜中这个炸弹就会被惩罚哦~</view>
        </view>
        <image src="http://admin.jlwp.vip/jjsq/icon_szzd@2x.png" style="width: 161rpx;height: 159rpx;" />
      </view>
      <view class="v2 flex items-center">
        <view class="flex-1">
          <view class="v3">指尖光圈</view>
          <view class="v4">你以为只是手指点点这么简单？~</view>
        </view>
        <image src="http://admin.jlwp.vip/jjsq/icon_shuzizd@2x.png" style="width: 159rpx;height: 159rpx;" />
      </view>
      <view class="grid">
        <view class="v5 flex column items-center">
          <text class="t1">大冒险</text>
          <image src="http://admin.jlwp.vip/jjsq/icon_dmx@2x.png" style="width: 127rpx;height: 112rpx;" />
        </view>
        <view class="v5 flex column items-center hot">
          <text class="t1">认怂书</text>
          <image src="http://admin.jlwp.vip/jjsq/icon_rss@2x.png" style="width: 111rpx;height: 119rpx;" />
        </view>
        <view class="v5 flex column items-center">
          <text class="t1">大转盘</text>
          <image src="http://admin.jlwp.vip/jjsq/icon_dzp@2x.png" style="width: 108rpx;height: 108rpx;" />
        </view>
      </view>
      <view class="t2">期待更多酒桌游戏~</view>
    </view>
  </view>
</template>

<script>
const statusBarHeight = uni.getSystemInfoSync().statusBarHeight + 'px'

export default {
  data() {
    return {
      statusBarHeight
    }
  },
  methods: {
    nav(url) {
      uni.navigateTo({ url })
    }
  }
}
</script>

<style scoped lang="scss">
.v1 {
  padding: 0 30rpx;
}

.v2 {
  width: 690rpx;
  height: 180rpx;
  background: #FFFFFF;
  border: 3px solid #000000;
  border-radius: 30rpx;
  padding: 0 50rpx;
  margin-bottom: 19rpx;
}

.v3 {
  font-size: 48rpx;
  font-weight: bold;
}

.v4 {
  font-size: 28rpx;
  margin-top: 16rpx;
}

.page {
  height: 100vh;
  background: #170a24;
  overflow: auto;
}

.title-text {
  display: flex;
  align-items: center;
  font-size: 28rpx;
  font-weight: bold;
  color: #fff;
  height: 44px;
  padding-left: 29rpx;
}

.t1 {
  font-size: 48rpx;
  font-weight: bold;
  padding: 30rpx 0 30rpx;
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  column-gap: 15rpx;
}

.v5 {
  height: 260rpx;
  border: 3px solid #000000;
  border-radius: 30rpx;
  background: url("http://admin.jlwp.vip/jjsq/bg_dmxty@2x.png") no-repeat;
  background-size: cover;
}

.t2 {
  color: #FFFFFF;
  padding: 45rpx 0 37rpx;
  text-align: center;
}

.hot {
  position: relative;

  &::before {
    content: '';
    position: absolute;
    width: 99rpx;
    height: 61rpx;
    background: url("http://admin.jlwp.vip/jjsq/HOT@2x.png") no-repeat;
    background-size: cover;
    left: 0;
    top: -26rpx;
  }
}
</style>
