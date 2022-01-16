<template>
	<view class="selector-body">
		<view class="hevu-slider-selector" @tap.stop @touchmove.stop>
			
			<view :class="`tiao ${silderValueShow ? 'show' : ''}`" ref='tiao' :style="{'--left': Math.min(makeUpBackLeft, makeUpBackRight) + 'px',
			  '--width': Math.abs(makeUpBackLeft - makeUpBackRight) + 'px', backgroundColor: bgColor,
			  '--bgColor': sliderSelectorColor, height: sliderHeight + 'rpx', borderRadius: sliderHeight / 2 + 'rpx',
			   '--height': sliderHeight, '--min': min, '--max': max}">
				   <view class="value" v-if='silderValueShow' :style="{height: sliderHeight + 'rpx',
						marginTop: -sliderHeight + 'rpx', fontSize:silderValueSize + 'rpx', color: silderValueColor}">
					   <view class="min">{{min + company}}</view>
					   <view class="max">{{max + company}}</view>
				   </view>
			   </view>
			  
			  <view :data-company='leftNumber + company' :class="`left ${selectorValueShow ? 'show' : ''} ${leftNumber < rightNumber ? 'after' : 'before'}`" ref='left' 
			  :style="{left: leftpercentage + '%', 
			   '--num': leftNumber, '--width': leftWidth, ...sliderStyle}"
			  	@touchstart="touchLeftStart" @touchmove='touchMove'></view>
			<view :data-company='rightNumber + company'  v-if='range' ref='right'
				:class="`right ${selectorValueShow ? 'show' : ''} ${leftNumber > rightNumber ? 'after' : 'before'}`"
				:style="{left: rightpercentage + '%',
				 '--num': rightNumber, '--width': rightWidth, ...sliderStyle}" 
				 @touchstart="touchStart"
				@touchend="touchEnd" @touchmove='touchMove'></view>
		</view>
		
	</view>


</template>

<script>
	/*
	 @property  {String} bgColor 滑块条背景颜色
	 @property  {Boolean} range 是否为范围选择
	 @property  {Number} max 滑块选择最大值
	 @property  {Number} min 滑块选择最小值
	 @property  {Array | Number} value 默认选择数值
	 @property  {String} company 数值单位
	 @property  {Number} toFixed 数值保留小数位数（小于0按0处理）
	
	@property  {Number} sliderHeight 滑动条高度
	@property  {Boolean} silderValueShow 选择器是否显示起始数值
	@property  {Number} silderValueSize 选择器显示起始数值字体大小
	@property  {String} silderValueColor 选择器显示起始数值字体颜色
	
	 @property  {Number} selectorSize 滑块大小
	 @property  {String} selectorColor 滑块按钮颜色
	 @property  {String} selectorValueColor 滑块选择数值颜色
	 @property  {Number} selectorValueSize  滑块选择数值字体大小
	 @property  {Boolean} selectorValueShow 滑块选择数值是否显示
	 @property  {String} sliderSelectorColor 选择数据内滑块背景颜色

	*/
	export default {
		name: 'hevu-slider-selector',
		props: {
			sliderSelectorColor: {
				type: String,
				default: '#3375f6'
			},
			bgColor: {
				type: String,
				default: '#eee'
			},
			selectorColor: {
				type: String,
				default: '#3375f6'
			},
			selectorValueColor: {
				type: String,
				default: '#000'
			},
			selectorValueSize: {
				type: Number,
				default: 30
			},
			range: {
				type: Boolean,
				default: false
			},
			max: {
				type: Number,
				default: 100
			},
			min: {
				type: Number,
				default: 0,
			},
			value: {
				type: Array | Number,
				default: 0,
			},
			selectorSize: {
				type: Number,
				default: 40,
			},
			sliderHeight: {
				type: Number,
				default: 20,
			},
			selectorValueShow: {
				type: Boolean,
				default: true
			},
			silderValueShow: {
				type: Boolean,
				default: false
			},
			silderValueSize: {
				type: Number,
				default: 22
			},
			silderValueColor: {
				type: String,
				default: '#000'
			},
			company: {
				type: String,
				default: ''
			},
			toFixed: {
				type: Number,
				default: 0,
			}
			
			
		},
		data() {
			return {
				makeUpBackLeft: 0,
				makeUpBackRight: 0,
				tiaoWidth: 0,
				leftWidth: 0,
				rightWidth: 0,
				key: 1
			}
		},
		computed: {
			leftNumber: function() { //滑块选择数值
				const max = this.max - this.min;
				const pow = Math.pow(10, this.toFixed < 0 ? 0 : this.toFixed);
				return Math.round(((this.makeUpBackLeft / (this.tiaoWidth)) * max + this.min) * pow) / pow || 0
			},
			rightNumber: function() { //滑块选择数值
				const max = this.max - this.min;
				const pow = Math.pow(10, this.toFixed < 0 ? 0 : this.toFixed);
				
				// 四舍五入保留指定小数
				return Math.round(((this.makeUpBackRight / (this.tiaoWidth)) * max + this.min) * pow) / pow || 0
			},
			leftpercentage: function(){ // 把px转换成百分比
				return this.makeUpBackLeft / this.tiaoWidth * 100;
			},
			rightpercentage: function(){ // 把px转换成百分比
				return this.makeUpBackRight / this.tiaoWidth * 100;
			},
			sliderStyle: function(){
				return {
					backgroundColor: this.selectorColor,
					width: this.selectorSize + 'rpx', 
					height: this.selectorSize + 'rpx',
					fontSize: this.selectorValueSize + 'rpx',
					lineHeight: this.selectorSize + 'rpx',
					transform: `translate(-50%, calc(-50% - (${this.sliderHeight / 2}rpx)))`,
					textAlign: 'center',
					'--color': this.selectorValueColor,
					'--size': this.selectorSize,
					
				}
			}
		},
		mounted() {
			this.$nextTick(function(){
				this.tiaoWidth = this.$refs.tiao.$el.getBoundingClientRect().width;
				this.leftWidth = this.$refs.left.$el.getBoundingClientRect().width;
				if(this.range){
					 this.rightWidth = this.$refs.right.$el.getBoundingClientRect().width;
				}
				const numLength = this.max - this.min;
				if(typeof this.value == 'number'){
					const left = ((this.value - this.min) / numLength) * this.tiaoWidth;
					
					this.makeUpBackLeft = left < 0 ? 0 : left >  this.tiaoWidth ? this.tiaoWidth : left;
					if(this.range){
						this.makeUpBackRight = left < 0 ? 0 : left >  this.tiaoWidth ? this.tiaoWidth : left;
					}
				} else {
					const left = ((this.value[0] - this.min) / numLength) * this.tiaoWidth;
					
					this.makeUpBackLeft = left < 0 ? 0 : left >  this.tiaoWidth - this.leftWidth ? this.tiaoWidth - this.leftWidth : left;
					if(this.range){
						const right = ((this.value[1] - this.min) / numLength) * this.tiaoWidth;
						this.makeUpBackRight = right < 0 ? 0 : right >  this.tiaoWidth ? this.tiaoWidth : right;
					}
				}
				
			})
			
		},
		methods: {
			touchLeftStart() {
				this.key = 1
				this.tiaoWidth = this.$refs.tiao.$el.getBoundingClientRect().width;
				this.leftWidth = this.$refs.left.$el.getBoundingClientRect().width;
			},
			touchStart(e) {
				this.key = 2
				this.rightWidth = this.$refs.right.$el.getBoundingClientRect().width;
				this.tiaoWidth = this.$refs.tiao.$el.getBoundingClientRect().width;
			},
			touchMove(e) {
				
				// 获取设置滑块距离左侧的px值
				if (this.key == 1) {
					// this.makeUpBackLeft = e.changedTouches[0].clientX < 0 ? 0 :
					// 	e.changedTouches[0].clientX > this.tiaoWidth - this.leftWidth ? this.tiaoWidth - this.leftWidth : e
					// 	.changedTouches[0].clientX;
					this.makeUpBackLeft = e.changedTouches[0].clientX < 0 ? 0 :
						e.changedTouches[0].clientX > this.tiaoWidth ? this.tiaoWidth : e
						.changedTouches[0].clientX;
				} else {
					// this.makeUpBackRight = e.changedTouches[0].clientX < 0 ? 0 :
					// 	e.changedTouches[0].clientX > this.tiaoWidth - this.rightWidth ? this.tiaoWidth - this.rightWidth :
					// 	e.changedTouches[0].clientX;
					this.makeUpBackRight = e.changedTouches[0].clientX < 0 ? 0 :
						e.changedTouches[0].clientX > this.tiaoWidth ? this.tiaoWidth :
						e.changedTouches[0].clientX;
				}
				this.$emit('onChange', this.range ? [this.leftNumber, this.rightNumber] : [this.leftNumber]);
			},
			touchEnd(e) {

			},
		}

	}
</script>

<style scoped lang="scss">
	.selector-body {
		padding: 20rpx;
	}

	.hevu-slider-selector {
		position: relative;
		padding: 20rpx 0;
		margin: 0 20rpx;

		.left,
		.right {
			position: absolute;
			width: calc(var(--size) * 1rpx);
			height: calc(var(--size) * 1rpx);
			
			width: 40rpx;
			height: 40rpx;
			border-radius: 50%;
			background-color: #3375f6;
			// top: 5rpx;
			z-index: 99;
			box-shadow: 0rpx 0rpx 15rpx #3375f6;
			&.show{
				&.after::after{
					// counter-reset: progress var(--num) ;
					// content: counters(progres);
					// content：: counters(progress, '') 'px';
					// 上面的也可以实现，不过px要写死
					
					content: '' attr(data-company);
					
					color: var(--color);
				}
				&.before::before{
					// counter-reset: progress var(--num);
					// content: counter(progress);
					
					content: '' attr(data-company);
					
					color: var(--color);
				}
			}
			
		}
		
		.right {
			z-index: 100;
		}

		.tiao {
			width: 100%;
			height: 10rpx;
			border-radius: 5rpx;
			background-color: #eee;
			position: relative;
			
			&::before {
				content: '';
				width: var(--width);
				margin-left: var(--left);
				display: block;
				height: 100%;
				border-radius: calc(var(--height) * .5 * 1rpx);
				background-color: var(--bgColor);
			}
			.value{
				display: flex;
				justify-content: space-between;
				align-items: center;
			}
		}
	}
</style>
