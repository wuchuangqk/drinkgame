<template>
  <view class="page-full page" @touchstart="touchstart" @touchend="touchend">
    <AppNavbar />
    <view class="v1">
      <view v-for="dice in diceList" :key="dice.x" class="rect"
        :style="{ left: dice.x, top: dice.y, zIndex: dice.zIndex }">
        <image v-if="dice.number !== -1" :src="`http://admin.jlwp.vip/jjsq/${dice.number}@2x.png`" class="dice" />
      </view>
    </view>
    <image src="http://admin.jlwp.vip/jjsq/zhong_ding@2x.png" class="zhong" :style="{ bottom: isOpen ? '45%' : '28%' }" />
    <view v-show="isOpen" class="dian flex center">总点数：{{ total }}</view>
    <view class="v2 flex items-center justify-between">
      <view>
        <image src="http://admin.jlwp.vip/jjsq/icon_jjds@2x.png" style="width: 123rpx;height: 118rpx;" />
      </view>
      <view @click="reStart">
        <image src="http://admin.jlwp.vip/jjsq/dianj_y@2x.png" style="width: 195rpx;height: 195rpx;" />
      </view>
      <view>
        <image src="http://admin.jlwp.vip/jjsq/icon_suoding@2x.png" style="width: 96rpx;height: 118rpx;" />
      </view>
    </view>
    <view v-show="isCanOpen" class="v3">
      <image src="http://admin.jlwp.vip/jjsq/haud@2x.png" style="width: 51rpx;height: 159rpx;" />
      <image src="http://admin.jlwp.vip/jjsq/shou@2x.png" style="width: 153rpx;height: 134rpx;" />
      <text class="t2">请往上滑动盅</text>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref, onBeforeMount } from 'vue'
import _ from 'lodash'
import AppNavbar from '@/components/app-navbar.vue';

class Dice {
  x: string
  y: string
  number: number = 1
  zIndex: number
  constructor(x, y, zIndex) {
    this.x = x
    this.y = y
    this.zIndex = zIndex
  }
}
const diceList = ref([
  new Dice('66rpx', '31rpx', 1),
  new Dice('133rpx', '47rpx', 1),
  new Dice('199rpx', '46rpx', 1),
  new Dice('264rpx', '46rpx', 1),
  new Dice('198rpx', '-2rpx', 0),
  new Dice('108rpx', '-6rpx', 0),
])
// 总点数
const total = ref(0)
const isOpen = ref(false)
const isCanOpen = ref(false)
// 重摇点数
const shuffle = () => {
  total.value = 0
  // 空位
  const emptyIndex = _.random(0, 5)
  diceList.value.forEach((dice, index) => {
    if (index === emptyIndex) {
      dice.number = -1
    } else {
      dice.number = _.random(1, 6)
      total.value += dice.number
    }
  })
}
const open = () => {
  shuffle()
  isCanOpen.value = false
  isOpen.value = true
}
const reStart = () => {
  isOpen.value = false
  setTimeout(() => {
    isCanOpen.value = true
  }, 1000)
}
let startY = 0
const touchstart = (e) => {
  const { clientY } = e.changedTouches[0]
  startY = clientY
}

const touchend = (e) => {
  const { clientY } = e.changedTouches[0]
  if (clientY < startY) {
    open()
  }
}
</script>

<style scoped lang="scss">
.page {
  position: relative;
  background: url("http://admin.jlwp.vip/jjsq/bg_fkytz@2x.jpg") no-repeat;
  background-size: 100% 100%;
}

.v1 {
  width: 383rpx;
  height: 202rpx;
  left: 50%;
  transform: translateX(-50%);
  background: url("http://admin.jlwp.vip/jjsq/zhongdi@2x.jpg") no-repeat;
  background-size: contain;
  position: absolute;
  bottom: 24%;
}

.start {
  position: absolute;
  bottom: 137rpx;
  width: 206rpx;
  height: 206rpx;
  left: 50%;
  transform: translateX(-50%);
}

.rect {
  width: 66rpx;
  height: 70rpx;
  position: absolute;
}

.dice {
  width: 100%;
  height: 100%;
}

.dian {
  width: 239rpx;
  height: 60rpx;
  background: rgba(0, 0, 0, 0.27);
  border-radius: 30rpx;
  text-stroke: 3px #000000;
  -webkit-text-stroke: 3px #000000;
  font-weight: bold;
  color: #FFFFFF;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 19%;
}

.v2 {
  position: absolute;
  bottom: 2%;
  padding: 0 70rpx;
  left: 0;
  right: 0;
}

.zhong {
  width: 307rpx;
  height: 381rpx;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 28%;
  transition: all 1s;
}

.v3 {
  position: absolute;
  left: 50%;
  top: 20%;
  animation: v3 2s linear infinite;

  .t2 {
    color: #fff;
    position: relative;
    left: -120rpx;
    top: 40rpx;
  }
}

@keyframes v3 {
  from {
    top: 22%;
  }

  90% {
    opacity: 1;
  }

  to {
    top: 10%;
    opacity: 0;
  }
}
</style>
