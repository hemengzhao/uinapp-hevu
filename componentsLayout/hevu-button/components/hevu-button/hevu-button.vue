<template>
	<view class="" :style="{
		width: width,
		height: height,
		transform: 'scale(0.99)',
	}">
		<button class='hevu-button' :loading='loading' :disabled='disabled' :style="{
			width: '100%',
			transform: 'scale(1.01)',
			height: height,
			lineHeight: height,
			color: fontColor,
			opacity: disabled ? (type !== 'purity' ? 0.4 : 0.5) : 1.0,
			backgroundColor: type === 'purity' ? color : (type === 'brief' ? RGBChange(color, .88, 'light') : 'rgba(0, 0, 0, 0)'),
			...allStyle,
			...getBorder(),
		}" @touchstart="touch" @tap.stop='onClick'>
			<slot></slot>
		</button>
	</view>
</template>

<script>
	/**
	 * @property  {String} width 按钮宽度
	 * @property  {String} height 按钮高度
	 * @property  {Array} radius 按钮圆角
	 * @property  {String} type 按钮类型  purity 纯色  brief 简约  hollow 镂空  none 无边框镂空
	 * @property  {Array ｜ number} borderSize 边框大小
	 * @property  {String} borderType 按钮边框的类型  solid：实线  dashed：虚线  dotted：点阵
	 * @property  {Boolean} disabled 是否禁用禁用
	 * @property  {Boolean} loading 是否加载状态
	 * @property  {String} boxShadow 按钮阴影
	 * 
	 * */
	export default {
		name: 'HevuButton',
		props: {
			width: {
				type: String,
				default: uni.getSystemInfoSync().screenWidth * 0.9 + 'px'
			},
			height: {
				type: String,
				default: '80rpx'
			},
			radius: {
				type: Array,
				default () {
					return ['5px']
				}
			},
			type: {
				type: String,
				default: 'purity'
			},
			color: {
				type: String,
				default: '#007aff'
			},
			fontColor: {
				type: String,
				default: '#000'
			},
			borderSize: {
				type: [Array, Number],
				default: 1
			},
			borderType: {
				type: String,
				default: 'solid'
			},
			disabled: {
				type: Boolean,
				default: false
			},
			loading: {
				type: Boolean,
				default: false
			},
			boxShadow: {
				type: String,
				default: ''
			},
		},
		computed: {
			allStyle: function(){
				const radius = this.getBorderRadius();
				return {
					borderTopLeftRadius: radius[0],
					borderTopRightRadius: radius[1],
					borderBottomRightRadius: radius[2],
					borderBottomLeftRadius: radius[3],
				}
			}
		},
		data(){
			return {
				
			}
		},
		
		methods: {
			touch(){
				
			},
			onClick(e){
				
				this.$emit('click', e);
			},
			getBorderRadius(){
				const arr = [...this.radius, ...this.radius, ...this.radius, ...this.radius].splice(0, 4);
				return arr;
			},
			getBorder(){
				let arr = [];
				if(typeof this.borderSize == 'number'){
					 arr = [this.borderSize, this.borderSize, this.borderSize, this.borderSize];
				} else {
					arr = [...this.borderSize, ...this.borderSize, ...this.borderSize, ...this.borderSize].splice(0, 4);
				}
				return {
					borderTop: this.type == 'none' ? 'none' :  arr[0]+ 'px ' + this.color + ' ' + this.borderType,
					borderRight: this.type == 'none' ? 'none' :  arr[1]+ 'px ' + this.color + ' ' + this.borderType,
					borderBottom: this.type == 'none' ? 'none' :  arr[2]+ 'px ' + this.color + ' ' + this.borderType,
					borderLeft: this.type == 'none' ? 'none' :  arr[3]+ 'px ' + this.color + ' ' + this.borderType,
				}
			},
			RGBChange(color, level, type) {
				// hex转rgb
				if (color.length === 4) {
					let arr = color.split('')
					color = '#' + arr[1] + arr[1] + arr[2] + arr[2] + arr[3] + arr[3]
				}
				let color16List = [color.substring(1, 3), color.substring(3, 5), color.substring(5, 7)]
				let r = parseInt(color16List[0], 16)
				let g = parseInt(color16List[1], 16)
				let b = parseInt(color16List[2], 16)
				let rgbc = [r, g, b]
				// 减淡或加深
				for (var i = 0; i < 3; i++)
					type === 'light' ? rgbc[i] = Math.floor((255 - rgbc[i]) * level + rgbc[i]) : rgbc[i] = Math.floor(rgbc[i] * (1 -
						level))
				// rgb转hex
				let R = rgbc[0].toString(16)
				let G = rgbc[1].toString(16)
				let B = rgbc[2].toString(16)
				if (R.length === 1) R = '0' + R
				if (G.length === 1) G = '0' + G
				if (B.length === 1) B = '0' + B
				return '#' + R + G + B
			},
		}
	}
</script>

<style lang="scss" scoped>
	.hevu-button{
		&::after{
			content: none;
			transform-origin: center;
			transform: scale(1.5);
		}
	}
</style>
