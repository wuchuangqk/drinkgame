<template>
	<view>
		<view class="slider-container1">
			<!-- <view class="flex"></view> -->
			<movable-area class="sliderBar">
				<!-- 进度条 -->
				<!-- <view class="progress" :style="{ width: x + 'px' }"></view> -->
				<movable-view class="slider" direction="horizontal" @change="onChange"></movable-view>
			</movable-area>
			<!-- <view :style="{ width: (minScore / maxScore) * 100 + '%' }"></view> -->
		</view>
	</view>
</template>

<script>
export default {
	props: {
		max: {
			type: Number,
			default: 10
		},
		min: {
			type: Number,
			default: 0
		}
	},
	data() {
		return {
			slideBarWidth: 0,
			minScore: this.min ? this.min : 0,
			maxScore: this.max ? this.max : 10,
			x: 0,
			y: 0,
			score: this.min ? this.min : 0,
		};
	},
	mounted() {
		var that = this;
		// 解决报错问题
		let el = uni.createSelectorQuery().in(this)
		this.$nextTick(() => {
			el.select(".slider-container").boundingClientRect(function (res) {
				that.slideBarWidth = res.width
			}).exec();
		})
	},
	methods: {
		onChange: function (e, i) {
			this.x = e.detail.x
			this.score = parseInt(this.x / this.slideBarWidth * this.maxScore)
			this.$emit('change', this.score)
		}
	}
}
</script>

<style lang="scss">
$uni-color-primary: #3A84FA;

.slider-container {
	display: flex;
	width: 100%;
	height: 32rpx;
	position: relative;

	&::before {
		content: '';
		position: absolute;
		height: 8rpx;
		border-radius: 8rpx;
		background-color: #EEEEEE;
		top: 50%;
		left: 0;
		transform: translateY(-50%);
		width: 100%;
	}

	.flex {
		flex: 1;
		height: 8rpx;
		border-radius: 8rpx 0 0 8rpx;
		background-color: $uni-color-primary;
		margin-top: 12rpx;
		position: relative;
		z-index: 1;
	}

	// .sliderBar {
	// 	height: 100%;
	// 	border-radius: 8rpx;
	// 	width: 100%;

	// 	.progress {
	// 		background-color: $uni-color-primary;
	// 		height: 100%;
	// 		position: absolute;
	// 		left: 0;
	// 		height: 8rpx;
	// 		top: 12rpx;
	// 		max-width: 100%;
	// 		z-index: 1;
	// 		border-radius: 0 8rpx 8rpx 0;
	// 	}

	// 	.slider {
	// 		width: 0;
	// 		height: 100%;
	// 		position: relative;
	// 		z-index: 2;

	// 		&::after {
	// 			content: '';
	// 			position: absolute;
	// 			border-radius: 16rpx;
	// 			background-color: $uni-color-primary;
	// 			width: 32rpx;
	// 			height: 100%;
	// 			transform: translatex(-50%);
	// 		}
	// 	}
	// }
}
</style>
