<template>
	<view class="content">
		
		<!-- <hevu-nav title='导航头' fixed :fixedTop='0' :extraHeight='0' search searchPlaceholderStyle='color:red'/>
		
		
		<view></view>
		<hevu-loading type="loading13" :opacity='0.8' :size="150">
			<image class="logo" src="/static/logo.png"></image>
		</hevu-loading>
		<HevuLoading type="loading13" :opacity='0.4' :loadingning='loadingning'>
			<view style="width: 750rpx;">
				<HevuSlidingVode></HevuSlidingVode>
			</view>
		</HevuLoading>
		<HevuButton @click='loadingning = !loadingning'>切换</HevuButton> -->
		
		<!-- <HevuGesture>
			<view class="touch">
				<HevuTabs :activeValue='1' type='back' @click='onCkikk'
				:list="['简约虚线', '镂空 点缀', '导航头123']"/>
				
			</view>
		</HevuGesture> -->
		<!-- <view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<HevuButton>纯色 实线</HevuButton>
		<br/>
		<HevuButton type="brief" borderType='dashed'>简约 虚线</HevuButton>
		<br/>
		<HevuButton type="hollow" borderType='dotted'>镂空  点缀</HevuButton>
		<br/>
		<HevuButton disabled loading>纯色 实线</HevuButton>
		<br/>
		<HevuButton disabled type="brief" borderType='dashed'>简约 虚线</HevuButton>
		<br/>
		<HevuButton disabled type="hollow" borderType='dotted' >镂空  点缀</HevuButton> -->
		
		<!-- <view :style="{width: '100%'}">
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading1" />
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading2"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading3"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading4"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading5"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading6"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading7"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading86"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading9"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading10"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading11"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading12" :size="200"/>
			</view>
			<view :style="{width: '33%', display: 'inline-block'}">
				<HevuLoading type="loading13" :size="150"/>
			</view>
		</view> -->
		
		<!-- <HevuLoading type="loading8" fixed /> -->
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
					url: '/pages/loading/index'
				}, {
					name: 'tabs选项卡',
					url: '/pages/loading/index'
				}, {
					name: '按钮',
					url: '/pages/loading/index'
				}, {
					name: '滑块选择器',
					url: '/pages/sliderSelector/index'
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
