<template>
  <view class="page-full page">
    <app-navbar />

    <app-dialog v-if="showRule" title="规则" @close="showRule = false">
      <view style="margin-top: 70rpx;">
        <view>
          鳄鱼拔牙游戏规则:游戏里有一只张着大嘴的鳄鱼！你可以和你的朋友一起。按下鳄鱼的牙齿。看看按到哪颗牙齿是危险的！
        </view>
        <view style="margin-top: 10px;">
          玩家依次点击鳄鱼嘴里的牙齿，其中有一颗牙齿按下后鳄鱼的嘴会咬下去。谁触发了鳄鱼咬下的机关谁就是需要被惩罚的玩家！!
        </view>
      </view>
    </app-dialog>
    <!-- 游戏结束 -->
    <view v-if="showEnd" class="end flex column items-center">
      <image src="/static/fahuo.png" class="end-img" />
      <view class="flex justify-center" style="margin-top: 95rpx;">
        <view class="btn primary" @click="restart">再来一局</view>
        <view class="btn second">选择惩罚</view>
      </view>
    </view>
  </view>
</template>
<script>
class Bomb {
  num
  show = true
  constructor(num) {
    this.num = num
  }
}
import _ from 'lodash'
export default {
  data() {
    return {
      bombList: [],
      answer: 0,
      showRule: true,
      showEnd: false,
    }
  },
  onLoad() {
    this.restart()
  },
  methods: {
    guess(bomb, index) {
      if (bomb.num < this.answer) {
        for (let i = 0; i <= index; i++) {
          this.bombList[i].show = false
        }
      } else if (bomb.num > this.answer) {
        for (let i = index; i < this.bombList.length; i++) {
          this.bombList[i].show = false
        }
      } else {
        // 爆炸
        this.showEnd = true
      }
    },
    restart() {
      this.showEnd = false
      this.answer = _.random(1, 100)
      this.bombList = new Array(100).fill(0).map((val, index) => {
        return new Bomb(index + 1)
      })
    }
  }
}
</script>

<style scoped lang="scss">
.page {
  position: relative;
  background: #07030b;
  overflow: auto;
}

.bomb {
  font-size: 32rpx;
  font-weight: 800;
  height: 100%;
  color: #fff;
  background: url("http://admin.jlwp.vip/jjsq/zhad_sm@2x.png") no-repeat;
  background-size: cover;
}

.grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  row-gap: 20rpx;
  padding: 15rpx 30rpx;
}

.grid-item {
  width: 113rpx;
  height: 128rpx;
}

.end {
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background: #000;
}

.v1 {
  width: 614rpx;
  height: 623rpx;
  background: url("http://admin.jlwp.vip/jjsq/guang.png") no-repeat;
  background-size: cover;

  .bomb {
    width: 230rpx;
    height: 261rpx;
    font-size: 67rpx;
    font-weight: 800;
    padding-top: 108rpx;
    padding-right: 18rpx;
    text-align: center;
  }
}

.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 300rpx;
  height: 70rpx;
  background: #F68B39;
  border: 3px solid #000000;
  border-radius: 45rpx;
  font-size: 30rpx;
  color: #fff;

  &.primary {
    background: #F68B39;
    margin-right: 44rpx;
  }

  &.second {
    background: #FF4D6A;
  }
}

.end-img {
  width: 749rpx;
  height: 1000rpx;
  margin: 0 auto;
}
</style>
