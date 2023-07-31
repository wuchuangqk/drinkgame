<template>
  <view class="page-full page">
    <app-navbar />
    <view>
      <view class="grid">
        <view v-for="(bomb, index) in bombList" :key="bomb.num" class="grid-item">
          <view v-show="bomb.show" class="bomb flex center" @click="guess(bomb, index)">{{ bomb.num }}</view>
        </view>
      </view>
    </view>
    <app-dialog v-if="showRule" title="规则" @close="showRule = false">
      <view style="margin-top: 70rpx;">
        <view>
          数字炸弹游戏规则:在一个数字范围内，有一个数字作为炸弹，谁猜中这个炸弹就被惩罚。
        </view>
        <view style="margin-top: 10px;">
          比如范围是1~99，炸弹是60，然后猜了一个数字是30，30不是炸弹，那么现在猜数字的范围就缩小到30~100，又猜了一个数字80.80也不是炸弹，那么现在又缩小范围到30~80，每次猜不能猜边界上的值，直到有人猜中这个炸弹，然后就受到惩罚。
        </view>
      </view>
    </app-dialog>
    <!-- 游戏结束 -->
    <view v-if="showEnd" class="end flex column items-center">
      <image src="/static/youxjs.png" style="width:544rpx;height:122rpx;margin-top: 20%;" />
      <view class="v1 flex center">
        <view class="bomb">{{ answer }}</view>
      </view>
      <view style="position: relative;top: -120rpx;">
        <view class="btn primary" @click="restart">再来一局</view>
        <view class="btn second">选择惩罚</view>
        <view class="btn primary">分享好友</view>
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
import AppNavbar from '@/components/app-navbar.vue';
export default {
  components: { AppNavbar },
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
  width: 550rpx;
  height: 90rpx;
  background: #F68B39;
  border: 3px solid #000000;
  border-radius: 45rpx;
  font-size: 30rpx;
  color: #fff;
  margin-bottom: 46rpx;

  &.primary {
    background: #F68B39;
  }

  &.second {
    background: #FF4D6A;
  }
}
</style>
