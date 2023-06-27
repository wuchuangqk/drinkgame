<template>
	<view class="page-full page">
		<view class="wrap">
			<image src="/static/bottle.png" class="bottle" :style="boxStyle" />
		</view>
		<view class="bottom">
			<button type="primary" data-eventsync="true" @click="start">开始</button>
		</view>
	</view>
</template>

<script setup lang="ts">
import { ref, onBeforeMount } from 'vue'
import _ from 'lodash'

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
}

.wrap {
	position: absolute;
	top: 10%;
	left: 50%;
	transform: translateX(-50%);
}

.bottle {
	width: 74px;
	height: 351px;
	transform: rotate(90deg);
}

.bottom {
	position: absolute;
	bottom: 20%;
	display: flex;
	justify-content: center;
}
</style>
