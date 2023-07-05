<template>
  <view class="page-full page">
    <view class="danmu" :style="textStyle">{{ danmu }}</view>
    <view class="panel">
      <view>
        <!-- <input type="range"> -->
        <!-- <SliderBar /> -->
        <movable-area class="movable-area">
          <movable-view class="movable-view" direction="horizontal"></movable-view>
        </movable-area>
      </view>
    </view>
    <view class="v1">
      <input type="text" v-model="inputText" class="input" placeholder="请输入">
      <button @click="changeDanmu">发送</button>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref, reactive, getCurrentInstance, nextTick } from 'vue'
import _ from 'lodash'
import { onReady, onUnload } from "@dcloudio/uni-app";
import SliderBar from '@/components/slider-bar.vue'

onReady(async () => {
  query = uni.createSelectorQuery().in(instance);
  const pageHeight = await getPageHeight()
  top = pageHeight
  // textStyle.top = pageHeight + 'px'
  // textRoll()
})
onUnload(() => {
  clearInterval(timer)
})

let query: any = null,
  pageHeight = 0,
  top = 0,
  timer: any = null
const instance = getCurrentInstance()
// 弹幕文字
const danmu = ref('这是字')
const textStyle = reactive({
  color: '#fff',
  fontSize: '80px',
  top: '0',
  transition: 'none',
})
const inputText = ref('')
// 文字滚动速度
const speed = 3

// 文字滚动
const textRoll = async () => {
  clearInterval(timer)
  const textHeight = await getTextHeight()
  timer = setInterval(() => {
    top -= speed
    // 当top小于自身高度时，意味着已经超出屏幕外
    if (top < -textHeight) {
      top = pageHeight
    }
    textStyle.top = top + 'px'
  }, 10)
}

// 获取页面高度
const getPageHeight = () => {
  return new Promise<number>((resolve) => {
    query.select('.page').boundingClientRect((data: any) => {
      resolve(data.height)
    }).exec();
  })
}
// 获取文本高度
const getTextHeight = () => {
  return new Promise<number>((resolve) => {
    query.select('.danmu').boundingClientRect((data: any) => {
      resolve(data.height)
    }).exec();
  })
}
// 设置新的弹幕
const changeDanmu = () => {
  danmu.value = inputText.value
  nextTick(() => {
    textRoll()
  })
}
</script>

<style scoped lang="scss">
.page {
  position: relative;
  background-color: rgb(0, 4, 0);
}

.danmu {
  position: absolute;
  left: 50%;
  transform: rotate(90deg);
  transform-origin: left;
  white-space: nowrap;
}

.v1 {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(255, 255, 255, 0.5);
  display: flex;

  .input {
    flex: 1;
    border: 1px solid #fff;
  }
}

.panel {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 10%;
  background-color: #140d20;
}

.movable-area {
  width: 100%;
}

.movable-view {
  background-color: red;
}
</style>
