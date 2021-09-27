<template>
	<view class="hevu-loading">
		<view class="hevu-loading-bag" :style="{opacity: opacity, backgroundColor: backgroundColor}"></view>
		<view class="hevu-loading-body">
			<view class="loafding">
				
				<LoadingBack1 v-if='type == "loading1"' :bacgColor='loadingIconColor' :size="size"/>
				<LoadingBack2 v-else-if='type == "loading2"' :bacgColor='loadingIconColor' :size="size"/>
				<LoadingBack3 v-else-if='type == "loading3"' :bacgColor='loadingIconColor' :size="size"/>
				<LoadingBack4 v-else-if='type == "loading4"' :bacgColor='loadingIconColor' :size="size"/>
				<LoadingBack5 v-else-if='type == "loading5"' :bacgColor='loadingIconColor' :size="size"/>
				<LoadingBack6 v-else-if='type == "loading6"' :bacgColor='loadingIconColor' :size="size"/>
				<LoadingBack7 v-else-if='type == "loading7"' :bacgColor='loadingIconColor' :size="size"/>
				<LoadingBack8 v-else-if='type == "loading8"' :bacgColor='loadingIconColor' :size="size"/>
				<LoadingBack9 v-else-if='type == "loading9"' :bacgColor='loadingIconColor' :size="size"/>
				<LoadingBack10 v-else-if='type == "loading10"' :bacgColor='loadingIconColor' :size="size"/>
			</view>
			<view class="loafdingText" :style="{fontSize: textSize + 'rpx', color: textColor}">
				{{loadingText}}
			</view>
		</view>
	</view>
</template>

<script>
	/*
		@property  {Number} opacity          背景透明度     1
		@property  {String} backgroundColor  背景颜色       #fff
	
		@property  {String} loadingText      加载文字提示   加载中....
		@property  {String} textColor        加载文字颜色   #000
		@property  {String} textSize         加载文字大小   30
		
		@property  {String} loadingIconColor 加载图颜色     #3375f6
		@property  {String} type             加载图类型     loading1
		@property  {Number} size             加载图大小     120
		
	*/
	import LoadingBack1 from './loadingBack/loading1.vue';
	import LoadingBack2 from './loadingBack/loading2.vue';
	import LoadingBack3 from './loadingBack/loading3.vue';
	import LoadingBack4 from './loadingBack/loading4.vue';
	import LoadingBack5 from './loadingBack/loading5.vue';
	import LoadingBack6 from './loadingBack/loading6.vue';
	import LoadingBack7 from './loadingBack/loading7.vue';
	import LoadingBack8 from './loadingBack/loading8.vue';
	import LoadingBack9 from './loadingBack/loading9.vue';
	import LoadingBack10 from './loadingBack/loading10.vue';
	export default {
		name: 'HevuLoading',
		props: {
			loadingText: {
				type: String,
				default: '加载中....'
			},
			textColor: {
				type: String,
				default: '#000'
			},
			textSize: {
				type: Number,
				default: 30
			},
			loadingIconColor: {
				type: String,
				default: '#3375f6'
			},
			type: {
				type: String,
				default: 'loading1'
			},
			opacity: {
				type: Number,
				default: 1,
			},
			backgroundColor: {
				type: String,
				default: '#FFF'
			},
			size: {
				type: Number,
				default: 200,
			}
		},
		data(){
			return {
				
			}
		},
		components: {
			LoadingBack1,
			LoadingBack2,
			LoadingBack3,
			LoadingBack4,
			LoadingBack5,
			LoadingBack6,
			LoadingBack7,
			LoadingBack8,
			LoadingBack9,
			LoadingBack10
		}
	}
</script>

<style lang="scss" scoped>
	.hevu-loading{
		position: fixed;
		z-index: 10000;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		.hevu-loading-bag{
			position: absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 100%;
			z-index: -1;
			background-color: #fff;
		}
		.hevu-loading-body{
		
			.loafding{
				padding: 20rpx;
			}
			.loafdingText{
				font-size: 30rpx;
				line-height: 60rpx;
				text-align: center;
			}
		}
	}
	
	@keyframes animate_1 {
		 30% {
			width: 30rpx;
			height: 70rpx;
		    transform: all .1s; 
		  }
		 45% {
		  	width: 20rpx;
		  	height: 50rpx;
		      transform: all .1s; 
		 }
	}
	@keyframes animate_2 {
		40% {
			width: 30rpx;
			height: 70rpx;
		    transform: all .1s; 
		  }
		  50% {
		   	width: 20rpx;
		   	height: 50rpx;
		       transform: all .1s; 
		  }
	}
	@keyframes animate_3 {
		 50% {
			width: 30rpx;
			height: 70rpx;
		    transform: all .1s; 
		 }
		  60% {
		   	width: 20rpx;
		   	height: 50rpx;
		       transform: all .1s; 
		  }
	}
	@keyframes animate_4 {
		
		60% {
			width: 30rpx;
			height: 70rpx;
			// -ms-transform: translate(80px,-60px) rotate(180deg);  
			//   	-webkit-transform: translate(80px,-60px) rotate(180deg);
		    transform: all .1s; 
		 }
		 70% {
		  	width: 20rpx;
		  	height: 50rpx;
		      transform: all .1s; 
		 }
	}
</style>
