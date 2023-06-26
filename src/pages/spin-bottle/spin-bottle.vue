<template>
	<view class="page-full page">
		<view class="box" :animation="animationData">
			<view class="arrow"></view>
		</view>
		<view class="bottom">
			<button type="primary" data-eventsync="true" @click="start">开始</button>
		</view>
	</view>
</template>

<script setup>
import { ref, onBeforeMount } from 'vue'
import _ from 'lodash'

onBeforeMount(() => {
	animationData.value = rotate.export()
})

// 定义一个动画
const animationData = ref()
const rotate = uni.createAnimation({
	duration: 2000,
	timingFunction: "ease",
})
const start = () => {
	console.log(1);
	rotate.rotate(360).step()
	rotate.rotate(_.random(0, 360)).step()
	animationData.value = rotate.export()
}
</script>

<style scoped lang="scss">
.page {
	position: relative;
}

.box {
	position: absolute;
	top: 10%;
	width: 600rpx;
	height: 200rpx;
	background: gray;
	left: 50%;
	transform: translateX(-50%);

	.arrow {
		width: 100rpx;
		height: 50rpx;
		position: absolute;
		background: red;
		top: 50%;
		transform: translateY(-50%);
		right: -50rpx;
	}
}

.bottom {
	position: absolute;
	bottom: 20%;
	display: flex;
	justify-content: center;
}
</style>
