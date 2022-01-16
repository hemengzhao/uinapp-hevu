<template>
	<view class="hevu-sliding-vode">
		<view class="slide" ref='slide'>
			<!-- require('./img.jpeg') -->
			<view class="top" :style="{backgroundImage: `url(${bgImg})`}">
				<view class="defectBack back" :style="{left: defectBackLeft + '%'}">
					
				</view>
				<view class="makeUpBack back" :style="{left: makeUpBackLeft + 'px', 
				'--left': -defectBackLeft + '%', '--bgImg': `url(${bgImg})`}">
					
				</view>
			</view>
			<!-- <HevuGesture @onTouchMove='onTouchMove' @onTouchEnd='onTouchEnd'> -->
				<view class="sliderBack">
					拖动滑块验证
					<view class="list" :style="{width: makeUpBackLeft + 'px'}"></view>
					<view class="rightBack" :style="{left: makeUpBackLeft + 'px'}" @touchstart="touchStart" @touchend="touchEnd" @touchmove='touchMove'>
						>>
					</view>
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
				disable: false,
			}
		},
		props: {
			type: {
				type: String,
				default: 'slide'
			},
			bgImg: {
				type: String,
				// default: 'http://nimg.ws.126.net/?url=http://dingyue.ws.126.net/2021/0323/cd092a59j00qqdyue000tc000hs00bec.jpg&thumbnail=650x2147483647&quality=80&type=jpg'
				default: require('./img.jpeg')
			},
			tolerance: { //缺口偏移容差
				type: Number,
				default: 5
			}
			
		},
		components: {
			HevuGesture,

		},
		methods: {
			touchStart(e){
				if(!this.disable){
					this.startX = e.touches[0].clientX;
					this.startY = e.touches[0].clientY;
					this.$emit('onTouchStart', this.info)
				}
				
			},
			touchMove(e){
				if(!this.disable){
					this.makeUpBackLeft = e.changedTouches[0].clientX - this.startX;
				}
				
			
			},
			touchEnd(e){
				if(this.disable){
					return
				}
				if(Math.abs(this.makeUpBackLeft - this.$refs.slide.$el.getBoundingClientRect().width * .56) < 5){
					this.disable = true;
					this.$emit('result', true)
				} else {
					this.$emit('result', false)
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
				// background-image: url(img.jpeg);
				background-size: 100% 100%;
				position: relative;
				.back{
					width: 80rpx;
					height: 80rpx;
					position: absolute;
					background-color: #eee;
					top: 40%;
					opacity: 0.8;
					border-radius: 10rpx;
					box-shadow: 0rpx 0rpx 30rpx #eee;
				}
				.makeUpBack{
					overflow: hidden;
					// background-image: var(--bgImg);
					&::before{
						 content: '';
						 opacity: 1;
						 background-image: var(--bgImg);
						 background-size: 100% 100%;
						 width: 750rpx;
						 height: 300rpx;
						 display: block;
						 transform: translate(var(--left), -40%)
					}
				}
				.defectBack{
					
				}
			}
			.sliderBack{
				width: 100%;
				height: 80rpx;
				line-height: 80rpx;
				font-size: 30rpx;
				text-align: center;
				background-color: rgba(225,225,225, 0.8);
				position: relative;
				.list{
					background-color: #4CD964;
					height: 100%;
					position: absolute;
					left: 0;
					top: 0;
				}
				.rightBack{
					position: absolute;
					width: 100rpx;
					height: calc(80rpx - 2px);
					border: 1px solid #999;
					background-color: #fff;
					left: 0;
					top: 0;
				}
			}
		}
	}
</style>
