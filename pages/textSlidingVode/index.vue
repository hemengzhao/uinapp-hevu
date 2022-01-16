<template>
	<view>
		<HevuNav title='验证码' rightIcon='' @leftTag='leftTag'/>
		
		<view class="topExhibition">
			<view style="text-align: center;">演示效果</view>
			
			<HevuTextSlidingVode ref='hevutextslidingvode' :isInsideCode='isInsideCode' :codeLength='codeLength' :isCodetypeNumber='isCodetypeNumber'
			:isCodeCasesensitive='isCodeCasesensitive' :identifyCode='identifyCode' :fontSizeMin='fontSizeMin'
			:fontSizeMax='fontSizeMax' :backgroundColorMin='backgroundColorMin' :backgroundColorMax='backgroundColorMax'
			:backgroundColor='backgroundColor' :colorMin='colorMin' :colorMax='colorMax'
			:lineColorMin='lineColorMin' :lineColorMax='lineColorMax' :dotColorMin='dotColorMin'
			:dotColorMax='dotColorMax' :isDot='isDot' :isLine='isLine'
			:contentWidth='contentWidth' :contentHeight='contentHeight' />
		</view>
		<view class="parameterSet">参数配置</view>
		<view class="parameter">
			
			<view class="list">
				<view class="name">画布宽度</view>
				<view class="setup">
					<HevuSliderSelector :value='contentWidth' :min='0' :max='255' @onChange='contentWidthFn'/>
					
				</view>
			</view>
			
			<view class="list">
				<view class="name">画布高度</view>
				<view class="setup">
					<HevuSliderSelector :value='contentHeight' :min='0' :max='255' @onChange='contentHeightFn'/>
					
				</view>
			</view>
			<view class="list">
				<view class="name">是否内部更新生成</view>
				<view class="setup">
					 <radio-group @change="isInsideCode = !isInsideCode">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="isInsideCode" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!isInsideCode" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			<view class="list">
				<view class="name">验证码长度</view>
				<view class="setup">
					<input type="number" v-model="codeLength" placeholder="请输入验证码长度" />
				</view>
			</view>
			<view class="list">
				<view class="name">验证码是否位纯数字</view>
				<view class="setup">
					 <radio-group @change="isCodetypeNumber = !isCodetypeNumber">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="isCodetypeNumber" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!isCodetypeNumber" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			<view class="list">
				<view class="name">验证码是否区分大小写</view>
				<view class="setup">
					 <radio-group @change="isCodeCasesensitive = !isCodeCasesensitive">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="isCodeCasesensitive" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!isCodeCasesensitive" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			
			<view class="list">
				<view class="name">验证设定</view>
				<view class="setup">
					<input type="text" v-model="identifyCode" placeholder="请输入背景颜色" />
				</view>
			</view>
			
			<view class="list">
				<view class="name">字体大小</view>
				<view class="setup">
					<HevuSliderSelector range :value='[fontSizeMin, fontSizeMax]' :min='12' :max='50' @onChange='fontSizeFn'/>
					
				</view>
			</view>
			<view class="list">
				<view class="name">字体颜色色值</view>
				<view class="setup">
					<HevuSliderSelector range :value='[colorMin, colorMax]' :min='0' :max='255' @onChange='colorFn'/>
					
				</view>
			</view>
			<view class="list">
				<view class="name">背景颜色</view>
				<view class="setup">
					<input type="text" v-model="backgroundColor" placeholder="请输入背景颜色" />
				</view>
			</view>
			<view class="list">
				<view class="name">背景颜色色值</view>
				<view class="setup">
					<HevuSliderSelector range :value='[backgroundColorMin, backgroundColorMax]' :min='0' :max='255' @onChange='backgroundColorMFn'/>
				</view>
			</view>
			<view class="list">
				<view class="name">是否需要干扰线</view>
				<view class="setup">
					 <radio-group @change="isLine = !isLine">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="isLine" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!isLine" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			
			<view class="list">
				<view class="name">干扰线颜色色值</view>
				<view class="setup">
					<HevuSliderSelector range :value='[lineColorMin, lineColorMax]' :min='0' :max='255' @onChange='lineColorFn'/>
					
				</view>
			</view>
			
			<view class="list">
				<view class="name">是否需要干扰点</view>
				<view class="setup">
					 <radio-group @change="isDot = !isDot">
						<label class="uni-list-cell uni-list-cell-pd" >
							<view style="display: inline-block;">
								<radio value="1" :checked="isDot" />
							</view>
							<view style="display: inline-block;">是</view>
						</label>
						<label class="uni-list-cell uni-list-cell-pd">
							<view style="display: inline-block;">
								<radio value="0" :checked="!isDot" />
							</view>
							<view style="display: inline-block;">否</view>
						</label>
					</radio-group>
				</view>
			</view>
			<view class="list">
				<view class="name">干扰点颜色色</view>
				<view class="setup">
					<HevuSliderSelector range :value='[dotColorMin, dotColorMax]' :min='0' :max='255' @onChange='dotColorFn'/>
					
				</view>
			</view>
			
			<view class="list">
				<view class="name">验证输入</view>
				<view class="setup">
					<input type="text" v-model="verificationText" placeholder="请输入背景颜色" />
					<button @click="verificationFn">验证</button>
				</view>
			</view>
		</view>
			
	</view>
</template>

<script>
	import HevuNav from "@/componentsLayout/hevu-nav/components/hevu-nav/hevu-nav.vue"
	import HevuTextSlidingVode from "@/componentsLayout/hevu-text-sliding-vode/components/hevu-text-sliding-vode/hevu-text-sliding-vode.vue"
	import HevuSliderSelector from "@/componentsLayout/hevu-slider-selector/components/hevu-slider-selector/hevu-slider-selector.vue"
	export default {
		data() {
			return {
				isInsideCode: false,
				codeLength: 4,
				isCodetypeNumber: false,
				isCodeCasesensitive: false,
				identifyCode: '1234',
				fontSizeMin: 35,
				fontSizeMax: 35,
				backgroundColor: '',
				backgroundColorMin: 180,
				backgroundColorMax: 240,
				colorMin: 50,
				colorMax: 160,
				lineColorMin: 100,
				lineColorMax: 200,
				dotColorMin: 0,
				dotColorMax: 255,
				isDot: true,
				isLine: true,
				contentWidth: 120,
				contentHeight: 40,
				
				verificationText: '',
			}
		},
		components: {
			HevuTextSlidingVode,
			HevuSliderSelector,
			HevuNav
		},
		computed: {
			vodeData: function(){
				const {isInsideCode,
				codeLength,
				isCodetypeNumber,
				isCodeCasesensitive,
				identifyCode,
				fontSizeMin,
				fontSizeMax,
				backgroundColor,
				backgroundColorMin,
				backgroundColorMax,
				colorMin,
				colorMax,
				lineColorMin,
				lineColorMax,
				dotColorMin,
				dotColorMax,
				isDot,
				isLine,
				contentWidth,
				contentHeight} = this;
				return {
					isInsideCode,
					codeLength,
					isCodetypeNumber,
					isCodeCasesensitive,
					identifyCode,
					fontSizeMin,
					fontSizeMax,
					backgroundColor,
					backgroundColorMin,
					backgroundColorMax,
					colorMin,
					colorMax,
					lineColorMin,
					lineColorMax,
					dotColorMin,
					dotColorMax,
					isDot,
					isLine,
					contentWidth,
					contentHeight
				}
			}
		},
		watch: {
			vodeData: {
				handler: function(e){
					this.$nextTick(function(){
						this.$refs.hevutextslidingvode.viewRefresh();
					})
					
				}
			}
		},
		methods: {
			verificationFn(){
				const type = this.$refs.hevutextslidingvode.verification(this.verificationText);
				alert(type ? '验证通过' : '验证失败')
			},
			
			leftTag(e){
				uni.navigateBack();
			},
			contentWidthFn(e){
			  this.contentWidth = e[0];
			},
			contentHeightFn(e){
			  this.contentHeight = e[0];
			},
			fontSizeFn(e){
			  this.fontSizeMin=e[0];
			  this.fontSizeMax=e[1];
			},
			colorFn(e){
			  this.colorMin=e[0];
			  this.colorMax=e[1];
			},
			backgroundColorMFn(e){
			  this.backgroundColorMin=e[0];
			  this.backgroundColorMax=e[1];
			},
			lineColorFn(e){
			  this.lineColorMin=e[0];
			  this.lineColorMax=e[1];
			},
			dotColorFn(e){
			  this.dotColorMin=e[0];
			  this.dotColorMax=e[1];
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
		text-align: center;
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

