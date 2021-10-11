<template>
	<view class="selector-body">
		<view class="hevu-slider-selector" @tap.stop @touchmove.stop>
			<view class="left" ref='left' :style="{left: makeUpBackLeft + 'px', backgroundColor: sliderColor}"
				@touchstart="touchLeftStart" @touchmove='touchMove'></view>
			<view class="tiao" ref='tiao' :style="{'--left': Math.min(makeUpBackLeft, makeUpBackRight)  + 'px',
			  '--width': Math.abs(makeUpBackLeft - makeUpBackRight) + 'px', backgroundColor: bgColor,
			  '--bgColor': selectorColor}"></view>
			<view class="right" v-if='range' ref='right'
				:style="{left: makeUpBackRight + 'px', backgroundColor: sliderColor}" @touchstart="touchStart"
				@touchend="touchEnd" @touchmove='touchMove'></view>
		</view>
		<view>
			left: {{leftNumber}}
		</view>
		<view>
			right: {{rightNumber}}
		</view>
	</view>


</template>

<script>
	/*
	 @property  {String} sliderColor 滑块按钮颜色
	 @property  {String} bgColor 滑块条背景颜色
	 @property  {String} selectorColor 选择滑块背景颜色
	 @property  {Boolean} range 范围选择
	*/
	export default {
		name: 'hevu-slider-selector',
		props: {
			sliderColor: {
				type: String,
				default: '#3375f6'
			},
			bgColor: {
				type: String,
				default: '#eee'
			},
			selectorColor: {
				type: String,
				default: '#3375f6'
			},
			range: {
				type: Boolean,
				default: false
			},
			max: {
				type: Number,
				default: 100
			},
			min: {
				type: Number,
				default: 0,
			},
			value: {
				type: Array,
				default: [100],
			}

		},
		data() {
			return {
				makeUpBackLeft: 0,
				makeUpBackRight: 0,
				tiaoWidth: 0,
				leftWidth: 0,
				rightWidth: 0,
				key: 1
			}
		},
		computed: {
			leftNumber: function() {
				const max = this.max - this.min;
				return Math.round((this.makeUpBackLeft / (this.tiaoWidth - this.leftWidth)) * max + this.min) || 0
			},
			rightNumber: function() {
				const max = this.max - this.min;
				return Math.round((this.makeUpBackRight / (this.tiaoWidth - this.rightWidth)) * max + this.min) || 0
			},
			
		},
		mounted() {
			console.log(this.value, 'val')
			this.makeUpBackLeft = this.value[0]
		},
		methods: {
			touchLeftStart() {
				this.key = 1
				this.tiaoWidth = this.$refs.tiao.$el.getBoundingClientRect().width;
				this.leftWidth = this.$refs.left.$el.getBoundingClientRect().width;
			},
			touchStart(e) {
				this.key = 2
				this.rightWidth = this.$refs.right.$el.getBoundingClientRect().width;
				this.tiaoWidth = this.$refs.tiao.$el.getBoundingClientRect().width;
			},
			touchMove(e) {
				if (this.key == 1) {
					this.makeUpBackLeft = e.changedTouches[0].clientX < 0 ? 0 :
						e.changedTouches[0].clientX > this.tiaoWidth - this.leftWidth ? this.tiaoWidth - this.leftWidth : e
						.changedTouches[0].clientX;

				} else {
					this.makeUpBackRight = e.changedTouches[0].clientX < 0 ? 0 :
						e.changedTouches[0].clientX > this.tiaoWidth - this.rightWidth ? this.tiaoWidth - this.rightWidth :
						e.changedTouches[0].clientX;

				}

				this.$emit('onChange', [this.makeUpBackLeft, this.makeUpBackRight]);
			},
			touchEnd(e) {

			},
		}

	}
</script>

<style scoped lang="scss">
	.selector-body {
		padding: 20rpx;
	}

	.hevu-slider-selector {
		position: relative;
		padding: 20rpx 0;
		margin: 0 20rpx;

		.left,
		.right {
			position: absolute;
			width: 40rpx;
			height: 40rpx;
			border-radius: 50%;
			background-color: #3375f6;
			top: 5rpx;
			z-index: 99;
			box-shadow: 0rpx 0rpx 15rpx #3375f6;
			;
		}

		.right {
			z-index: 100;
		}

		.tiao {
			width: 100%;
			height: 10rpx;
			border-radius: 5rpx;
			background-color: #eee;

			&::before {
				content: '';
				width: var(--width);
				margin-left: var(--left);
				display: block;
				height: 10rpx;
				background-color: var(--bgColor);
			}
		}
	}
</style>
