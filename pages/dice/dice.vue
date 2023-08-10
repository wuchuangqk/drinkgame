<template>
  <view class="page-full page" @touchstart="touchstart" @touchmove="touchmove" @touchend="touchend">
    <AppNavbar />
    <view class="v1">
      <view v-for="dice in diceList" :key="dice.x" class="rect"
        :style="{ left: dice.x, top: dice.y, zIndex: dice.zIndex }">
        <image v-if="dice.number !== -1" :src="`http://admin.jlwp.vip/jjsq/${dice.number}@2x.png`" class="dice" />
      </view>
    </view>
    <view class="zhong-wrap" :style="{ top: top }">
      <image src="http://admin.jlwp.vip/jjsq/zhong_ding@2x.png" class="zhong" :class="{ shake }" />
    </view>
    <view v-show="showDice" class="dian flex center">总点数：{{ total }}</view>
    <view v-show="!shake" class="v2 flex items-center justify-between">
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

<script>
import _ from 'lodash'
import AppNavbar from '@/components/app-navbar.vue';
class Dice {
  x
  y
  number
  zIndex
  constructor(x, y, zIndex) {
    this.x = x
    this.y = y
    this.zIndex = zIndex
  }
}
const MAX_DIS = 100
export default {
  components: { AppNavbar },
  data() {
    return {
      diceList: [
        new Dice('56rpx', '31rpx', 1),
        new Dice('123rpx', '47rpx', 1),
        new Dice('189rpx', '46rpx', 1),
        new Dice('254rpx', '46rpx', 1),
        new Dice('188rpx', '-2rpx', 0),
        new Dice('98rpx', '-6rpx', 0),
      ],
      total: 0,
      showDice: false, // 骰子点数
      isCanOpen: true,
      startY: 0,
      shake: false, // 晃动动画
      top: '48%',
      origin: '', // 盅的原点
      lastPosition: '', // 记录盅最后一次移动到的位置
      touchmove: null,
    }
  },
  onLoad() {
    this.touchmove = _.throttle(this.touchmove1, 50)
  },
  onReady() {
    const query = uni.createSelectorQuery().in(this);
    query.selectAll('.zhong-wrap').boundingClientRect(data => {
      const statusBarHeight = uni.getSystemInfoSync().statusBarHeight
      this.lastPosition = this.origin = data[0].top + statusBarHeight
    }).exec();
    this.shuffle()
  },
  methods: {
    back() {
      uni.navigateBack()
    },
    // 重摇点数
    shuffle() {
      this.total = 0
      // 空位
      const emptyIndex = _.random(0, 5)
      this.diceList.forEach((dice, index) => {
        if (index === emptyIndex) {
          dice.number = -1
        } else {
          dice.number = _.random(1, 6)
          this.total += dice.number
        }
      })
    },
    // 重新开始
    reStart() {
      // 盅复位
      this.top = this.origin + 'px'
      this.showDice = false
      this.isCanOpen = false
      this.shake = true
      setTimeout(() => {
        this.shuffle()
        this.isCanOpen = true
        this.shake = false
      }, 1000)
    },
    touchstart(e) {
      if (!this.isCanOpen) return
      const { clientY } = e.changedTouches[0]
      this.startY = clientY
    },
    touchmove1(e) {
      if (!this.isCanOpen) return
      // 掀开盅时，显示骰子点数
      this.showDice = true
      const { clientY } = e.changedTouches[0]
      // 计算移动距离
      const dis = this.startY - clientY
      if (this.lastPosition - dis < this.origin - MAX_DIS) {
        this.top = this.origin - MAX_DIS + 'px'
      } else if (this.lastPosition - dis > this.origin) {
        this.top = this.origin + 'px'
      } else {
        this.top = this.lastPosition - dis + 'px'
      }
      // 盅回到原位，隐藏骰子点数
      if (parseFloat(this.top) === this.origin) {
        this.showDice = false
      }
    },
    touchend(e) {
      if (!this.isCanOpen) return
      this.lastPosition = parseFloat(this.top)
    }
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
  background: url("http://admin.jlwp.vip/jjsq/zhongdi.png") no-repeat;
  background-size: contain;
  position: absolute;
  top: 63%;
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

.zhong-wrap {
  width: 307rpx;
  height: 381rpx;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}

.zhong {
  width: 100%;
  height: 100%;
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

@keyframes shake {
  0% {
    transform: rotate(10deg);
  }

  35% {
    transform: rotate(-10deg);
  }

  60% {
    transform: rotate(10deg);
  }

  100% {
    transform: rotate(-10deg);
  }
}

.shake {
  animation: shake 0.6s;
  animation-iteration-count: 3;
  animation-direction: alternate;
}
</style>
