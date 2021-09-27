<template>
	<view @touchstart="touchStart" @touchend="touchEnd" @touchmove='touchMove'>
		<slot></slot>
		<view>
			startX: {{startX}}<br/>
			startY: {{startY}}<br/>
			endX: {{endX}}<br/>
			endY: {{endY}}<br/>
			X轴移动: {{startX - endX}}<br/>
			Y轴移动: {{startY - endY}}<br/>
		</view>
	</view>
</template>

<script>
	
	// 手势操作判断
	export default {
		name: 'HevuGesture',
		data(){
			return {
				startX: 0,
				startY: 0,
				endX: 0,
				endY: 0,
				moveX: 0,
				moveY: 0,
			}
		},
		props: {
			
		},
		computed: {
			info: function(){
				return {
					startX: this.startX,
					startY:  this.startY,
					endX:  this.endX,
					endY:  this.endY,
					moveX:  this.endX - this.startX,
					moveY:  this.endY - this.endY,
				}
			}
		},
		methods: {
			//当手指触摸屏幕时候触发，即使已经有一个手指放在屏幕上也会触发
			touchStart(e){
				// console.log(e)
				this.startX = e.touches[0].clientX;
				this.startY = e.touches[0].clientY;
				this.$emit('onTouchStart', this.info)
			},
			// 当手指从屏幕上离开的时候触发
			touchEnd(e){
				console.log(e)
				this.endX = e.changedTouches[0].clientX;
				this.endY = e.changedTouches[0].clientY;
				this.$emit('onTouchEnd', this.info)
			},
			// 当手指在屏幕上滑动的时候连续地触发。在这个事件发生期间，调用preventDefault()事件可以阻止滚动。
			touchMove(e){
				console.log(e)
				this.endX = e.touches[0].clientX;
				this.endY = e.touches[0].clientY;
				this.$emit('onTouchMove', this.info);
			}
		}
	}
</script>

<style>
</style>
