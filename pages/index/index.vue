<template>
	<view class="content">
		<HevuNavlist :list="list" @onChange="onChange"/>
	</view>
</template>

<script>
	import HevuButton from "@/componentsLayout/hevu-button/components/hevu-button/hevu-button.vue"
	import HevuTabs from '@/componentsLayout/hevu-tabs/components/hevu-tabs/hevu-tabs.vue'
	import HevuGesture from '@/componentsLayout/hevu-gesture/components/hevu-gesture/hevu-gesture.vue'
 	import HevuSlidingVode from '@/componentsLayout/hevu-sliding-vode/components/hevu-sliding-vode/hevu-sliding-vode.vue'
	import HevuLoading from '@/componentsLayout/hevu-loading/components/hevu-loading/hevu-loading.vue'
	import HevuNavlist from '@/componentsLayout/hevu-navlist/components/hevu-navlist/hevu-navlist.vue'
	
	export default {
		data() {
			return {
				title: 'Hello',
				loadingning: true,
				list: [{
					name: 'loading',
					url: '/pages/loading/index'
				}, {
					name: '自定义导航头',
					url: '/pages/nav/index'
				}, {
					name: 'tabs选项卡',
					url: '/pages/tabs/index'
				}, {
				// 	name: '按钮',
				// 	url: '/pages/loading/index'
				// }, {
					name: '滑块选择器',
					url: '/pages/sliderSelector/index'
				}, {
					name: '图片验证码',
					url: '/pages/slidingVode/index'
				}, {
					name: '验证码',
					url: '/pages/textSlidingVode/index'
				}]
				
			}
		},
		components: {
			HevuButton,
			HevuTabs,
			HevuGesture,
			HevuSlidingVode,
			HevuLoading,
			HevuNavlist
		},
		onLoad() {

		},
		methods: {
			onCkikk(ien,e){
				console.log(ien,e)
			},
			touchStart(e){
				
			},
			touchmove(e){
				
			},
			touchEnd(e){
				
			},
			
			onChange(iten, k){
				
				// uni.navigateTo({
				//     url: iten.url
				// });
				console.log(iten, k);
			}
		}
	}
</script>

<style>
	.content {
		/* display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center; */
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	.touch{
		width: 300rpx;
		height: 300px;
		background-color: #4CD964;
	}
</style>
