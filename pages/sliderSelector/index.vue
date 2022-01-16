<template>
	<view>
		<HevuNav title='滑块选择器' rightIcon='' @leftTag='leftTag'/>
		<view class="topExhibition">
			<view style="text-align: center;">演示效果</view>
			<HevuSliderSelector v-if='show' :range='range' :silderValueShow='silderValueShow' :selectorValueShow='selectorValueShow'
			:sliderHeight='sliderHeight' :selectorSize='selectorSize' :toFixed='toFixed' :company='company'/>
		</view>
		<view class="parameterSet">参数配置</view>
		<view class="parameter">
			<view class="list">
				<view class="name">范围选择</view>
				<view class="setup">
					 <radio-group @change="range = !range">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="range" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!range" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			<view class="list">
				<view class="name">展示滑动条起始数值</view>
				<view class="setup">
					 <radio-group @change="silderValueShow = !silderValueShow">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="silderValueShow" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!silderValueShow" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			<view class="list">
				<view class="name">展示选择数值</view>
				<view class="setup">
					 <radio-group @change="selectorValueShow = !selectorValueShow">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="selectorValueShow" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!selectorValueShow" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			
			<view class="list">
				<view class="name">滑块选择器滑动条高度</view>
				<view class="setup">
					<HevuSliderSelector :value='sliderHeight' :min='10' :max='40' @onChange='onChangeSliderHeight'/>
					
				</view>
			</view>
			
			<view class="list">
				<view class="name">滑块大小</view>
				<view class="setup">
					<HevuSliderSelector :value='selectorSize' :min='20' :max='80' @onChange='onChangeSelectorSize'/>
					
				</view>
			</view>
			<view class="list">
				<view class="name">保留小数</view>
				<view class="setup">
					<HevuSliderSelector :value='toFixed' :min='0' :max='8' @onChange='onChangeToFixed'/>
					
				</view>
			</view>
			<view class="list">
				<view class="name">单位</view>
				<view class="setup">
					 <input class="uni-input" placeholder="输入框" v-model="company" />
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
				company: '',
				selectorSize: 40,
				sliderHeight: 20,
				toFixed: 0,
				selectorValueShow: true,
				silderValueShow: false,
				range: false,
				show: true,
				
			}
		},
		components: {
			HevuNav,
			HevuSliderSelector
		},
		watch:{
			range: function(e){
				this.show = false
				setTimeout(() => {
					this.show = true
				}, 100)
			}
		},
		methods: {
			leftTag(){
				uni.navigateBack()
			},
			onChangeSelectorSize(e){
				this.selectorSize = e[0];
			},
			onChangeSliderHeight(e){
				this.sliderHeight = e[0];
			},
			onChangeToFixed(e){
				this.toFixed = e[0];
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

