<template>
  <view class="page-full page">
    <AppNavbar />
    <view>
      <view class="grid">
        <view v-for="(bomb, index) in bombList" :key="bomb.num" class="grid-item">
          <view v-show="bomb.show" class="bomb flex center" @click="guess(bomb, index)">{{ bomb.num }}</view>
        </view>
      </view>
    </view>
    <AppDialog title="规则"></AppDialog>
  </view>
</template>

<script setup lang="ts">
import { ref, onBeforeMount } from 'vue'
import _ from 'lodash'
import AppNavbar from '@/components/app-navbar.vue';
import AppDialog from '@/components/app-dialog.vue';

onBeforeMount(() => {
  restart()
})

class Bomb {
  num: number
  show: boolean = true
  constructor(num: number) {
    this.num = num
  }
}

const bombList = ref<Bomb[]>([])
let answer = 0
const guess = (bomb: Bomb, index: number) => {
  if (bomb.num < answer) {
    for (let i = 0; i <= index; i++) {
      bombList.value[i].show = false
    }
  } else if (bomb.num > answer) {
    for (let i = index; i < bombList.value.length; i++) {
      bombList.value[i].show = false
    }
  } else {
    // 爆炸
  }
}
const restart = () => {
  answer = _.random(1, 100)
  bombList.value = new Array(100).fill(0).map((val, index) => {
    return new Bomb(index + 1)
  })
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
</style>
