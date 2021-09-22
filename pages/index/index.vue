<template>
	<view class="content">
		<hevu-nav title='导航头' fixed :fixedTop='0' :extraHeight='0' search searchPlaceholderStyle='color:red'/>
		
		<image class="logo" src="/static/logo.png"></image>
		<HevuTabs :activeValue='3'
		:list="['简约 虚线', '镂空  点缀', 12, '导航头123', 34, '简约 虚线', '镂空  点缀', '纯色 实线', '导航头', '导航头123']"/>
		<br/>
		<HevuTabs :activeValue='1' :animated='false'
		:list="['简约虚线', '镂空 点缀', '导航头123']"/>
		<br/>
		<HevuTabs :activeValue='1' type='back' @click='onCkikk'
		:list="['简约虚线', '镂空 点缀', '导航头123']"/>
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
	</view>
</template>

<script>
	import HevuButton from "@/componentsLayout/hevu-button/components/hevu-button/hevu-button.vue"
	import HevuTabs from '@/componentsLayout/hevu-tabs/components/hevu-tabs/hevu-tabs.vue'
 	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		components: {
			HevuButton,
			HevuTabs
		},
		onLoad() {

		},
		methods: {
onCkikk(ien,e){
	console.log(ien,e)
}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
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
</style>
