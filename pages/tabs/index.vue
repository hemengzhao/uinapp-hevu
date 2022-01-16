<template>
	<view>
		<HevuNav title='滑块选择器' rightIcon='' @leftTag='leftTag'/>
		<view class="topExhibition">
			<view style="text-align: center;">演示效果</view>
			<HevuTabs :activeValue='1' :animated='animated' :type='type ? "line" : "back"'
			 :list="['简约', '虚线', '镂空', '点缀']" backColor='#ff0'/>
		</view>
		<view class="parameterSet">参数配置</view>
		<view class="parameter">
			<view class="list">
				<view class="name">tabs类型</view>
				<view class="setup">
					 <radio-group @change="type = !type">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="type" />
							</view>
							<view style="display: inline-block;">line</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!type" />
							</view>
							<view style="display: inline-block;">back</view>
						</label>
					</radio-group>
				</view>
			</view>
			<view class="list">
				<view class="name">下划线动画</view>
				<view class="setup">
					 <radio-group @change="animated = !animated">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="animated" />
							</view>
							<view style="display: inline-block;">开启</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!animated" />
							</view>
							<view style="display: inline-block;">关闭</view>
						</label>
					</radio-group>
				</view>
			</view>
			
		</view>
			
	</view>
</template>

<script>
	import HevuNav from "@/componentsLayout/hevu-nav/components/hevu-nav/hevu-nav.vue"
	import HevuTabs from '@/componentsLayout/hevu-tabs/components/hevu-tabs/hevu-tabs.vue'
	import HevuSliderSelector from "@/componentsLayout/hevu-slider-selector/components/hevu-slider-selector/hevu-slider-selector.vue"
	export default {
		data() {
			return {
				animated: true,
				type: true,
			}
		},
		components: {
			HevuNav,
			HevuSliderSelector,
			HevuTabs
		},
		methods: {
			leftTag(){
				uni.navigateBack()
			},
		}
	}
</script>

<style scoped lang="scss">
.topExhibition{
		padding: 20rpx 20rpx ;
		border: 1px dashed #999;
		margin: 20rpx;
		border-radius: 10rpx;
		height: 300rpx;
	}
	.parameterSet{
		text-align: center;
		line-height: 60rpx;
		border-bottom: 1px dashed #999;
		margin-bottom: 20rpx;
	}
	.parameter{
		max-height: calc(100vh - 530rpx - 44px);
		overflow: auto;
		
		.list{
			padding:15rpx 0 15rpx 20rpx;
			&:nth-child(odd){
				// background-color: #bbb;
			}
			&:nth-child(even){
				background-color: #eee;
			}
			.name{
				height: 50rpx;
				line-height: 50rpx;
				&::before{
					content: ' ';
					display: inline-block;
					width: 15rpx;
					height: 50rpx;
					border-radius: 6rpx;
					background-color: #F0AD4E;
					vertical-align: bottom;
					margin-right: 20rpx;
				}
			}
			.setup{
				margin-top: 15rpx;
				.uni-list-cell{
					display: inline-block;
					text-align: center;
					margin-right: 20rpx;
				}
				.uni-input{
					
					height: 60rpx;
					line-height: 60rpx;
					margin:0 20rpx;
				}
			}
		}
	}
</style>
