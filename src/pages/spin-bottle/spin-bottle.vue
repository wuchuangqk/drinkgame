<template>
	<view class="page-full page">
		<AppNavbar />
		<view class="wrap">
			<image src="/static/jiuping@2x.png" class="bottle" :style="boxStyle" />
		</view>
		<image src="/static/zhuan@2x.png" class="start" data-eventsync="true" @click="start" />
	</view>
</template>

<script setup lang="ts">
import { ref, onBeforeMount } from 'vue'
import _ from 'lodash'
import AppNavbar from '@/components/app-navbar.vue';

onBeforeMount(() => {
})

const boxStyle = ref<any>({})
let deg = 0
const start = () => {
	// 转3圈加一圈随机
	const fixedDeg = 360 * 3
	const randomDeg = _.random(0, 360)
	deg += fixedDeg + randomDeg
	boxStyle.value = {
		transition: 'all 3s ease',
		transform: `rotate(${deg}deg)`
	}
}
</script>

<style scoped lang="scss">
.page {
	position: relative;
	background: url("/static/bg_zpz@2x.png") no-repeat;
	background-size: 100% 100%;
}

.wrap {
	position: absolute;
	top: 10%;
	left: 50%;
	transform: translateX(-50%);
}

.bottle {
	width: 242rpx;
	height: 784rpx;
	// transform: rotate(90deg);
}

.start {
	position: absolute;
	bottom: 137rpx;
	width: 206rpx;
	height: 206rpx;
	left: 50%;
	transform: translateX(-50%);
}
</style>
