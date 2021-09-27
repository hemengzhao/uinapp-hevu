<template>
	<view class="hevu-sliding-vode">
		<view class="slide" ref='slide'>
			<!-- require('./img.jpeg') -->
			<view class="top" :style="{backgroundImg: 'url(./img.jpeg)'}">
				<view class="defectBack back" :style="{left: defectBackLeft + '%'}">
					
				</view>
				<view class="makeUpBack back" :style="{left: makeUpBackLeft + 'px'}">
					
				</view>
			</view>
			<!-- <HevuGesture @onTouchMove='onTouchMove' @onTouchEnd='onTouchEnd'> -->
				<view class="sliderBack">
					<view class="list" :style="{width: makeUpBackLeft + 'px'}"></view>
					<view class="rightBack" :style="{left: makeUpBackLeft + 'px'}" @touchstart="touchStart" @touchend="touchEnd" @touchmove='touchMove'></view>
				</view>
			<!-- </HevuGesture> -->
			
		</view>
	</view>
</template>

<script>
	import HevuGesture from '@/componentsLayout/hevu-gesture/components/hevu-gesture/hevu-gesture.vue'
	export default {
		name: 'HevuSlidingVode',
		data(){
			return {
				defectBackLeft: 56,
				makeUpBackLeft: 0,
				startX: 0,
				startY: 0,
			}
		},
		props: {
			type: {
				type: String,
				default: 'slide'
			},
			bgImg: {
				type: String,
				default: ''
			}
		},
		components: {
			HevuGesture,
		},
		methods: {
			touchStart(e){
				// console.log(e)
				this.startX = e.touches[0].clientX;
				this.startY = e.touches[0].clientY;
				this.$emit('onTouchStart', this.info)
			},
			touchMove(e){
				this.makeUpBackLeft = e.changedTouches[0].clientX - this.startX;
			
			},
			touchEnd(e){
				console.log(this.$refs.slide.$el.getBoundingClientRect().width)
				console.log(this.$refs.slide.$el.getBoundingClientRect().width * .56)
				if(Math.abs(this.makeUpBackLeft - this.$refs.slide.$el.getBoundingClientRect().width * .56) < 20){
					alert('验证成功')
				} else {
					alert('验证失败')
					this.makeUpBackLeft = 0
				}
			},
			onclick(){
				console.log('sdas')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.hevu-sliding-vode{
		width: 100%;
		.slide{
			.top{
				width: 100%;
				height: 300rpx;
				background-image: url(img.jpeg);
				background-size: 100% 100%;
				position: relative;
				.back{
					width: 80rpx;
					height: 80rpx;
					position: absolute;
					background-color: #eee;
					top: 40%;
					opacity: 0.8;
					&::before{
						content: '';
						display: block;
						width: 40rpx;
						height: 40rpx;
						border-radius: 50%;
						background-color: #eee;
						position: absolute;
						top: -35rpx;
						left: 18rpx;
					}
					&::after{
						content: '';
						width: 40rpx;
						height: 40rpx;
						border-radius: 50%;
						background-color: #eee;
						display: block;
						position: absolute;
						right: -35rpx;
						top: 22rpx;
					}
					
				}
				.defectBack{
					
				}
			}
			.sliderBack{
				width: 100%;
				height: 80rpx;
				background-color: rgba(225,225,225, 0.8);
				position: relative;
				.list{
					background-color: #4CD964;
					height: 100%;
				}
				.rightBack{
					position: absolute;
					width: 80rpx;
					height: 80rpx;
					background-color: red;
					left: 0;
					top: 0;
				}
			}
		}
	}
</style>
