<template>
	<view style="overflow: hidden">
		<HevuNav title='loading' rightIcon='' @leftTag='leftTag'/>
		
		<view class="topExhibition">
			<view style="text-align: center;">演示效果</view>
			<HevuLoading :loadingning='loadingning' :fixed='fixed' :zIndex='zIndex' :opacity='opacity' 
			:backgroundColor='backgroundColor' :loadingText='loadingText' :textColor='textColor'
			:textSize='textSize' :textFlicker='textFlicker' :loadingIconColor='loadingIconColor'
			:type='`loading${type}`' :size='size'>
				<view style="line-height: 100px;">这是一个dom节点</view>
			</HevuLoading>
		</view>
		<view class="parameterSet">参数配置</view>
		<view class="parameter">
			<view class="list">
				<view class="name">加载状态</view>
				<view class="setup">
					 <radio-group @change="radioChange">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="loadingning" />
							</view>
							<view style="display: inline-block;">显示</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!loadingning" />
							</view>
							<view style="display: inline-block;">隐藏</view>
						</label>
					</radio-group>
				</view>
			</view>
			<view class="list">
				<view class="name">固定定位</view>
				<view class="setup">
					 <radio-group @change="fixedChange">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="fixed" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!fixed" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			
			<view class="list">
				<view class="name">定位层级</view>
				<view class="setup">
					<HevuSliderSelector :value='zIndex' :max='9999' @onChange='onChangeIndex'/>
					
				</view>
			</view>
			
			<view class="list">
				<view class="name">背景透明度</view>
				<view class="setup">
					<HevuSliderSelector :value='opacity' :max='1' :toFixed='1' @onChange='onChangeOpacity'/>
					
				</view>
			</view>
			<view class="list">
				<view class="name">背景颜色</view>
				<view class="setup">
					 <input class="uni-input" placeholder="输入框" v-model="backgroundColor" />
				</view>
			</view>
			
			<view class="list">
				<view class="name">加载文字提示</view>
				<view class="setup">
					 <input class="uni-input" placeholder="输入框" v-model="loadingText" />
				</view>
			</view>
			
			<view class="list">
				<view class="name">加载文字颜色</view>
				<view class="setup">
					 <input class="uni-input" placeholder="输入框" v-model="textColor" />
				</view>
			</view>
			
			<view class="list">
				<view class="name">加载文字大小</view>
				<view class="setup">
					<HevuSliderSelector :min='10' :value='textSize' :max='50' @onChange='onChangeTextSize'/>
				</view>
			</view>
			
			<view class="list">
				<view class="name">加载文字闪动</view>
				<view class="setup">
					 <radio-group @change="textFlickerChange">
					 	<label class="uni-list-cell uni-list-cell-pd" >
					 		<view style="display: inline-block;">
					 			<radio value="1" :checked="fixed" />
					 		</view>
					 		<view style="display: inline-block;">是</view>
					 	</label>
					 	<label class="uni-list-cell uni-list-cell-pd">
					 		<view style="display: inline-block;">
					 			<radio value="0" :checked="!fixed" />
					 		</view>
					 		<view style="display: inline-block;">否</view>
					 	</label>
					 </radio-group>
				</view>
			</view>
			
			<view class="list">
				<view class="name">加载图颜色</view>
				<view class="setup">
					 <input class="uni-input" placeholder="输入框" v-model="loadingIconColor" />
				</view>
			</view>
			
			<view class="list">
				<view class="name">加载图类型</view>
				<view class="setup">
					<HevuSliderSelector :min='1' :max='13' :value='type' @onChange='onChangeType'/>
					
				</view>
			</view>
			
			<view class="list">
				<view class="name">加载图大小</view>
				<view class="setup">
					<HevuSliderSelector :min='50' :max='200' :value='size' @onChange='onChangeSize' bgColor='#fff'/>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import HevuLoading from '@/componentsLayout/hevu-loading/components/hevu-loading/hevu-loading.vue'
	import HevuNav from "@/componentsLayout/hevu-nav/components/hevu-nav/hevu-nav.vue"
	import HevuSliderSelector from "@/componentsLayout/hevu-slider-selector/components/hevu-slider-selector/hevu-slider-selector.vue"
	export default {
		data() {
			return {
				loadingning: true,
				fixed: false,
				zIndex: 10001,
				opacity: .6,
				backgroundColor: '#fff',
				loadingText: '加载中....',
				textColor: '#3375f6',
				textSize: 30,
				textFlicker: false,
				loadingIconColor: '#3375f6',
				type: 1,
				size: 120
			}
		},
		components: {
			HevuLoading,
			HevuNav,
			HevuSliderSelector
		},
		methods: {
			radioChange(e){
				console.log(e.detail.value)
				this.loadingning = e.detail.value == 1;
			},
			fixedChange(e){
				this.fixed = e.detail.value == 1;
				if(e.detail.value == 1){
					setTimeout(() => {
						this.fixed = false;
					}, 3000);
				}
			},
			textFlickerChange(e){
				this.textFlicker =  e.detail.value == 1;
			},
			leftTag(){
				uni.navigateBack()
			},
			onChangeIndex(e){
				this.zIndex = e[0];
			},
			onChangeOpacity(e){
				this.opacity = e[0];
			},
			onChangeTextSize(e){
				this.textSize = e[0]
			},
			onChangeType(e){
				this.type = e[0]
			},
			onChangeSize(e){
				this.size = e[0]
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
