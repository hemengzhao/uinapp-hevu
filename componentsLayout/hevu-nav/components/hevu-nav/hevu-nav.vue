<template>
	<view :class="{'he-navs': true, 'he-navs-fixed': fixed}" :style="{top: fixedTop + 'px'}">
		<view class="heNav-bg" :style="{backgroundColor: bgColor, opacity: opacity}">
			
		</view>
		<!-- 额外的高度 -->
		<view v-if='extraHeight' :style="{height: extraHeight + 'px'}"></view>
		<view class="heNav" :style="{color: color}">
			<!-- 左侧按钮 -->
			<view class="heNav-left" @tap="leftTag">
				
				<uni-icons v-if='leftIcon.length' :color="color" :type="leftIcon" size="28"></uni-icons>
				<text v-else-if='leftText.length'>{{leftText}}</text>
				
			</view>
			<!--中间内容 -->
			<view class="heNav-con" @tap="contTag">
				<text>{{title}}</text>
				
				<!-- 搜索导航 -->
				<input :class="`uni-input searchInput ${searchShow ? 'show' : ''}`"
				:placeholder-style='searchPlaceholderStyle' :style='searchStyle'
					@input='searchInput' @confirm='searchConfirm' v-model="searchValue"
				 :confirm-type="confirmType" :placeholder="searchPlaceholder" />
				<uni-icons class="clear" @click="searchValue = ''" v-if='searchShow && searchValue.length' type="clear" size="22"></uni-icons>
			</view>
			<!-- 右侧按钮 -->
			<view class="heNav-right" @tap="rightTag">
				<!-- 搜索导航 -->
				<uni-icons v-if='search && !searchShow' :color="color" type="search" size="28"></uni-icons>
				<text v-else-if='search && searchShow'>取消</text>
				
				<uni-icons v-else-if='rightIcon.length' :color="color" :type="rightIcon" size="28"></uni-icons>
				<text v-else-if='rightText.length'>{{rightText}}</text>
			</view>
		</view>
	</view>
	
</template>

<script>
	/**
	 * @description 导航栏组件，主要用于头部导航
	 * @property  {String} title 导航名字
	 * @property  {String} color 字体颜色
	 * @property  {String} bgColor 背景颜色
	 * @property  {String} rightIcon 右侧icon图标
	 * @property  {String} rightText 右侧文字
	 * @property  {String} leftIcon 左侧icon图标
	 * @property  {String} leftText  左侧文字
	 * @property  {String} leftText  左侧文字
	 *  icon > 文字
	 *  @property  {number} opacity  背景透明度 0 - 1
	 *  @property  {boolean} fixed  是否固定
	 *  @property  {number} fixedTop  固定导航top值
	 *  @property  {number} extraHeight  文字上方是否增加额外的高度(包含在导航头内部)
	 *  @property  {boolean} search  是否为搜索导航头 
	 *  @property  {String} confirmType  搜索导航头键盘右下角按钮文字 (跟随uinapp输入框)  send 发送   search  搜索  next 下一个 go 前往  done 完成   
	 *  @property  {String} searchPlaceholder  搜索导航头输入框为空时占位符
	 * @property  {String} searchPlaceholderStyle  指定 placeholder 的样式
	 * @property  {Object} searchStyle  指定搜索框样式
	 * 
	 * @property leftTag {function} 左侧点击事件
	 * @property rightTag {function} 右侧点击事件
	 * @property contTag {function} 中间点击事件
	 * @property searchInput {function} 搜索导航输入框输入变化事件 返回输入框值
	 * @property searchConfirm {function} 搜索导航输入框点击搜索事件 返回输入框值
	 * @ 
	 */
	export default {
		
		name: 'HevuNav',
		props: {
			title: {
				type: String,
				default: ''
			},
			color: {
				type: String,
				default: '#fff'
			},
			bgColor: {
				type: String,
				default: '#3375f6'
			},
			
			rightIcon: {
				type: String,
				default: 'scan'
			},
			rightText: {
				type: String,
				default: ''
			},
			leftIcon: {
				type: String,
				default: 'back'
			},
			leftText: {
				type: String,
				default: ''
			},
			opacity: {
				type: Number,
				default: 1,
			},
			fixed: {
				type: Boolean,
				default: false
			},
			fixedTop: {
				type: Number,
				default: 0,
			},
			extraHeight: {
				type: Number,
				default: 0,
			},
			search: {
				type: Boolean,
				default: false
			},
			confirmType: {
				type: String,
				default: 'search'
			},
			searchPlaceholder: {
				type: String,
				default: '请输入搜索内容'
			},
			searchPlaceholderStyle: {
				type: String,
				default: ''
			},
			searchStyle: {
				type: Object,
				default: () => {}
			}
		},
		data() {
			return {
				searchShow: false,
				searchValue: '',
			}
		},
		mounted() {
			
		},
		components: {
		},
		methods: {
			leftTag(){
				this.$emit("leftTag");
			},
			rightTag(){
				if(this.search){
					this.searchShow = !this.searchShow;
					if(this.searchShow){
						this.searchValue = ''
					}
				} else {
					this.$emit("rightTag");
				}
				
			},
			contTag(){
				this.$emit("contTag");
			},
			searchInput(){
				this.$emit('searchInput', e.detail.value);
			},
			searchConfirm(){
				this.$emit('searchConfirm', e.detail.value);
			}
		}
	}
</script>

<style lang="scss" scoped>
	.he-navs{
		width: 100%;
		position: relative;
		&.he-navs-fixed{
			position: fixed;
			top: 0;
		}
		.heNav-bg{
			position: absolute;
			z-index: -1;
			width: 100%;
			height: 100%;
			left: 0;
			top: 0;
		}
		.heNav{
			background-color: transparent;
			width: 100%;
			display: flex;
			justify-content: space-between;
			align-items: center;
			height: 44px;
			align-items: center;
			font-size: 34rpx;
			// line-height: 44px;
			&-left{
				max-width: 150rpx;
				text-align: left;
				margin-left: 20rpx;
				
			}
			&-con{
				flex: 1;
				text-align: center;
				white-space: nowrap;
				overflow: hidden;
				margin: 0 20rpx;
				position: relative;
				height: 100%;
				line-height: 44px;
				.searchInput{
					position: absolute;
					margin: 0 5px;
					right: -750rpx;
					top: 7px;
					width: calc(100% - 55px);
					height: 30px;
					line-height: 30px;
					border-radius: 15px;
					background: #fff;
					transition: all .3s;
					color: #333;
					padding: 0 30px 0 15px;
					&.show{
						right: 0;
					}
				}
				.clear{
					position: absolute;
					right: 20rpx;
					
				}
			}
			&-right{
				max-width: 150rpx;
				text-align: right;
				margin-right: 20rpx;
			}
		}
		
	}
	
</style>
<style>
	
</style>
