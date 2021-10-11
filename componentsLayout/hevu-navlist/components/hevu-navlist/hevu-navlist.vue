<template>
	<view class="hevu-navlist">
		<navigator :url='item.url' v-for="(item, k) in list" :key='k' class="navlist" @click="change(item, k)">
			<text>{{typeof item == 'string' || typeof item.name == 'number' ? item : item.name}} </text>
			<uni-icons type="arrowright" />
		</navigator>
	</view>
</template>

<script>
	export default{
		name: 'HevuNavlist',
		props: {
			list: {
				type: Array,
				default: []
			}
		},
		data(){
			return {
				
			}
		},
		methods: {
			change(change, k){
				this.$emit('onChange', change, k)
			}
		}
	}
</script>

<style scoped lang="scss">
	.hevu-navlist{
		.navlist{
			line-height: 60rpx;
			// text-align: left;
			font-size: 28rpx;
			padding: 20rpx 20rpx ;
			border-bottom: 1px solid #eee ;
			position: relative;
			display: flex;
			justify-content: space-between;
			// &:last-child{
			// 	border-bottom: none;
			// }
			
		}
	}
</style>
