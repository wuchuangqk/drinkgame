<template>
	<view class="page-full page">
		<AppNavbar />
		<view class="wrap">
			<image src="http://admin.jlwp.vip/jjsq/jiuping@2x.png" class="bottle" :style="{ transform: `rotate(${deg}deg)` }" />
		</view>
		<image src="http://admin.jlwp.vip/jjsq/zhuan@2x.png" class="start" @click="start" />
	</view>
</template>

<script>
import _ from 'lodash'
import AppNavbar from '@/components/app-navbar.vue';
let deg = 0
export default {
	data() {
		return {
			boxStyle: {},
			deg: 0,
			flag: false,
		}
	},
	methods: {
		start() {
			// 避免重复点击
			if (this.flag) return
			this.flag = true
			// 固定转3圈，加一圈随机角度
			const fixedDeg = 360 * 3
			const randomDeg = _.random(0, 360)
			this.deg += fixedDeg + randomDeg
			setTimeout(() => {
				this.flag = false
			}, 3000);
		}
	}
}
</script>

<style scoped lang="scss">
.page {
	position: relative;
	background: url("http://admin.jlwp.vip/jjsq/bg_zpz@2x.jpg") no-repeat;
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
	transition: all 3s ease;
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
