<template>
	<view class="section">
		<view class='sk-wave' :style="{width: size + 'rpx', height: size * (2/3) + 'rpx'}">
		  <view class='sk-rect sk-rect-1' :style="backStyle"></view>
		  <view class='sk-rect sk-rect-2' :style="backStyle"></view>
		  <view class='sk-rect sk-rect-3' :style="backStyle"></view>
		  <view class='sk-rect sk-rect-4' :style="backStyle"></view>
		  <view class='sk-rect sk-rect-5' :style="backStyle"></view>
		</view>
	</view>
	
</template>

<script>
	
	export default {
		name: "LoadingBack3",
		props: {
			bacgColor: {
				type: String,
				default: '#3375f6'
			},
			size: {
				type: Number,
				default: 200,
			}
			
		},
		computed: {
			backStyle: function(){
				return {
					backgroundColor: this.bacgColor,
					width: this.size / 12 + 'rpx'
				}
			}
		},
		data(){
			return{
				
			}
		}
	}
</script>

<style scoped lang="scss">
	.sk-wave {
	  width: 6em;
	  height: 4em;
	  margin: auto;
	  text-align: center;
	  font-size: 1em;
	}
	.sk-wave .sk-rect {
	  height: 100%;
	  width: .5em;
	  margin-right: 10rpx;
	  display: inline-block;
	  -webkit-animation: sk-wave-stretch-delay 1.2s infinite ease-in-out;
	          animation: sk-wave-stretch-delay 1.2s infinite ease-in-out;
	  &:last-child{
		  margin-right: 0rpx;
	  }
	}
	
	//animation-delay 属性定义动画何时开始
	.sk-wave .sk-rect-1 {
	  -webkit-animation-delay: -1.2s;
	          animation-delay: -1.2s;
	}
	.sk-wave .sk-rect-2 {
	  -webkit-animation-delay: -1.1s;
	          animation-delay: -1.1s;
	}
	.sk-wave .sk-rect-3 {
	  -webkit-animation-delay: -1s;
	          animation-delay: -1s;
	}
	.sk-wave .sk-rect-4 {
	  -webkit-animation-delay: -0.9s;
	          animation-delay: -0.9s;
	}
	.sk-wave .sk-rect-5 {
	  -webkit-animation-delay: -0.8s;
	          animation-delay: -0.8s;
	}
	
	@-webkit-keyframes sk-wave-stretch-delay {
	  0%, 40%, 100% {
	    -webkit-transform: scaleY(0.4);
	            transform: scaleY(0.4);
	  }
	  20% {
	    -webkit-transform: scaleY(1);
	            transform: scaleY(1);
	  }
	}
	
	@keyframes sk-wave-stretch-delay {
	  0%, 40%, 100% {
	    -webkit-transform: scaleY(0.4);
	            transform: scaleY(0.4);
	  }
	  20% {
	    -webkit-transform: scaleY(1);
	            transform: scaleY(1);
	  }
	}
	
</style>
