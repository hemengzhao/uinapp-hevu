<template>
	<view class="heNav" :style="{color: color, backgroundColor: bgColor}">
		<view>{{leftText}}</view>
		<view>{{title}}</view>
		<view>{{rightText}}</view>
	</view>
</template>

<script>
	
	export default {
		
		name: 'HeNav',
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
				default: ''
			},
			rightText: {
				type: String,
				default: '前进'
			},
			leftIcon: {
				type: String,
				default: 'back'
			},
			leftText: {
				type: String,
				default: '后退'
			}
			
		},
		data() {
			return {
				
			}
		},
		mounted() {
			
		},
		components: {
		},
		methods: {
			clickLeft(){
				this.$emit("clickLeft");
			},
			clickRight(){
				this.$emit("clickRight");
			},
		}
	}
</script>

<style lang="scss" scoped>
	.heNav{
		width: 100%;
		display: flex;
		justify-content: space-between;
		height: 44px;
		align-items: center;
	}
</style>
<style>
	
</style>
