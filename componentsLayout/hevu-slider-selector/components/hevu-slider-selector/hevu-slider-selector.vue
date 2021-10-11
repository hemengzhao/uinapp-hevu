<template>
	<view class="selector-body">
		<view class="hevu-slider-selector" @tap.stop @touchmove.stop>
			
			<view class="tiao" ref='tiao' :style="{'--left': Math.min(makeUpBackLeft, makeUpBackRight) + 'px',
			  '--width': Math.abs(makeUpBackLeft - makeUpBackRight) + 'px', backgroundColor: bgColor,
			  '--bgColor': selectorColor, height: sliderHeight + 'rpx', borderRadius: sliderHeight / 2 + 'rpx',
			   '--height': sliderHeight}"></view>
			  
			  <view :class="`left ${leftNumber < rightNumber ? 'after' : 'before'}`" ref='left' 
			  :style="{left: leftpercentage + '%', 
			   '--num': leftNumber, '--width': leftWidth, ...sliderStyle}"
			  	@touchstart="touchLeftStart" @touchmove='touchMove'></view>
			<view :class="`right ${leftNumber > rightNumber ? 'after' : 'before'}`" v-if='range' ref='right'
				:style="{left: rightpercentage + '%',
				 '--num': rightNumber, '--width': rightWidth, ...sliderStyle}" 
				 @touchstart="touchStart"
				@touchend="touchEnd" @touchmove='touchMove'></view>
		</view>
		<view>
			left: {{leftNumber}}
		</view>
		<view>
			right: {{rightNumber}}
		</view>
	</view>


</template>

<script>
	/*
	 @property  {String} sliderColor 滑块按钮颜色
	 @property  {String} bgColor 滑块条背景颜色
	 @property  {String} selectorColor 选择滑块背景颜色
	 @property  {String} numberColor 滑块选择数值颜色
	 @property  {Number} numberSize  滑块选择数值字体大小
	 @property  {String} selectorColor 选择滑块背景颜色
	 @property  {String} selectorColor 选择滑块背景颜色
	 @property  {Boolean} range 范围选择
	 @property  {Number} max 滑块选择最大值
	 @property  {Number} min 滑块选择最小值
	 @property  {Array | Number} value 默认选择大小
	 @property  {Number} size 滑块大小
	 @property  {Number} sliderHeight 滑动条高度
	  
	*/
	export default {
		name: 'hevu-slider-selector',
		props: {
			sliderColor: {
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
			numberColor: {
				type: String,
				default: '#000'
			},
			numberSize: {
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
				default: 30,
			},
			size: {
				type: Number,
				default: 40,
			},
			sliderHeight: {
				type: Number,
				default: 10,
			},
			
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
			leftNumber: function() {
				const max = this.max - this.min;
				return Math.round((this.makeUpBackLeft / (this.tiaoWidth)) * max + this.min) || 0
			},
			rightNumber: function() {
				const max = this.max - this.min;
				return Math.round((this.makeUpBackRight / (this.tiaoWidth)) * max + this.min) || 0
			},
			leftpercentage: function(){ // 把px转换成百分比
				return this.makeUpBackLeft / this.tiaoWidth * 100;
			},
			rightpercentage: function(){ // 把px转换成百分比
				return this.makeUpBackRight / this.tiaoWidth * 100;
			},
			sliderStyle: function(){
				return {
					backgroundColor: this.sliderColor,
					width: this.size + 'rpx', 
					height: this.size + 'rpx',
					fontSize: this.numberSize + 'rpx',
					lineHeight: this.size + 'rpx',
					transform: `translate(-50%, calc(-50% - (${this.sliderHeight / 2}rpx)))`,
					textAlign: 'center',
					'--color': this.numberColor,
					'--size': this.size, 
				}
			}
		},
		mounted() {
			console.log(this.value, 'val')
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

				this.$emit('onChange', [this.makeUpBackLeft, this.makeUpBackRight]);
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
			
			&.after::after{
				counter-reset: progress var(--num);
				content: counter(progress);
				// margin-left: calc(var(--width) * 1px);
				color: var(--color);
			}
			&.before::before{
				counter-reset: progress var(--num);
				content: counter(progress);
				// margin-left: calc(var(--width) * (-.5px));
				color: var(--color);
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

			&::before {
				content: '';
				width: var(--width);
				margin-left: var(--left);
				display: block;
				height: 100%;
				background-color: var(--bgColor);
			}
		}
	}
</style>
