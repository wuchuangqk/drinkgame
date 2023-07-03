<template>
  <view class="page-full page">
    <view class="content" :style="textStyle">{{ content }}</view>
    <view class="v1">
      <input type="text" v-model="text" class="input" placeholder="请输入">
      <button @click="play">发送</button>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref, onBeforeMount, reactive, getCurrentInstance, nextTick } from 'vue'
import _ from 'lodash'
import { onReady, onUnload } from "@dcloudio/uni-app";

onBeforeMount(() => {
})
onReady(async () => {
  query = uni.createSelectorQuery().in(instance);
  // 获取页面高度
  query.select('.page').boundingClientRect((data: any) => {
    pageHeight = data.height
  }).exec();
  top = pageHeight
  textStyle.top = pageHeight + 'px'
  f1()
})
onUnload(() => {
  clearInterval(timer)
})
let query
const f1 = async () => {
  clearInterval(timer)
  const width = await getWidth()
  timer = setInterval(() => {
    top -= speed
    // console.log(width, top);

    if (top < -width) {
      top = pageHeight
    }
    textStyle.top = top + 'px'
  }, 10)
}
// 重新获取高度
const getWidth = () => {
  return new Promise<number>((resolve) => {
    query.select('.content').boundingClientRect((data: any) => {
      console.log(data);
      resolve(data.height)
    }).exec();
  })
}
const instance = getCurrentInstance()
let pageHeight = 0
let top = 0

let deg = 0
const content = ref('这是字')
const textStyle = reactive({
  color: '#fff',
  fontSize: '80px',
  top: '0',
  transition: 'none',
})
const text = ref('')
const play = () => {
  content.value = text.value
  nextTick(() => {
    f1()
  })
}
const speed = 3
let timer
</script>

<style scoped lang="scss">
.page {
  position: relative;
  background-color: rgb(0, 4, 0);
}

.content {
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
</style>
