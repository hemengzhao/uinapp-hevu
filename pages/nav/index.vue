<template>
	<view>
		<HevuNav title='自定义导航头' rightIcon='' @leftTag='leftTag'/>
		<view class="topExhibition">
			<view style="text-align: center;">演示效果</view>
			<HevuNav :title='title' rightIcon='' :rightText='rightText' :bgColor='bgColor' :color='color' :extraHeight='extraHeight' :search='search' :opacity='opacity'/>
		</view>
		
		<view class="parameterSet">参数配置</view>
		<view class="parameter">
			<view class="list">
				<view class="name">是否为搜索导航头</view>
				<view class="setup">
					 <radio-group @change="search = !search">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="search" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!search" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			
			
			<view class="list">
				<view class="name">背景透明度</view>
				<view class="setup">
					<HevuSliderSelector :value='opacity' :max='1' :toFixed='1' @onChange='onChangeOpacity'/>
					
				</view>
			</view>
			
			<view class="list">
				<view class="name">文字上方增加额外的高度</view>
				<view class="setup">
					<HevuSliderSelector :value='extraHeight' :max='60' @onChange='onChangeExtraHeight'/>
					
				</view>
			</view>
			<view class="list">
				<view class="name">背景颜色</view>
				<view class="setup">
					 <input class="uni-input" placeholder="输入框" v-model="bgColor" />
				</view>
			</view>
			
			<view class="list">
				<view class="name">导航文字文字</view>
				<view class="setup">
					 <input class="uni-input" placeholder="输入框" v-model="title" />
				</view>
			</view>
			<view class="list">
				<view class="name">导航右侧文字</view>
				<view class="setup">
					 <input class="uni-input" placeholder="输入框" v-model="rightText" />
				</view>
			</view>
			<view class="list">
				<view class="name">文字颜色</view>
				<view class="setup">
					 <input class="uni-input" placeholder="输入框" v-model="color" />
				</view>
			</view>
		</view>
	
	</view>
</template>

<script>
	import HevuNav from "@/componentsLayout/hevu-nav/components/hevu-nav/hevu-nav.vue"
	import HevuSliderSelector from "@/componentsLayout/hevu-slider-selector/components/hevu-slider-selector/hevu-slider-selector.vue"
	export default {
		data() {
			return {
				title: '导航名字',
				color: '#fff',
				bgColor: '#3375f6',
				opacity: 1,
				rightText: '右侧文字',
				extraHeight: 0,
				search: false,
				
			}
		},
		components: {
			HevuNav,
			HevuSliderSelector
		},
		methods: {
			leftTag(){
				uni.navigateBack()
			},
			onChangeOpacity(e){
				this.opacity = e[0]
			},
			onChangeExtraHeight(e){
				this.extraHeight = e[0]
			}
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
