<template>
	<view>
		<HevuNav title='滑动验证' rightIcon='' @leftTag='leftTag'/>
		<HevuSlidingVode/>
	</view>
</template>

<script>
	import HevuNav from "@/componentsLayout/hevu-nav/components/hevu-nav/hevu-nav.vue"
	import HevuSlidingVode from "@/componentsLayout/hevu-sliding-vode/components/hevu-sliding-vode/hevu-sliding-vode.vue"
	export default {
		data() {
			return {
				
			}
		},
		components: {
			HevuSlidingVode,
			HevuNav
		},
		methods: {
			leftTag(e){
				uni.navigateBack();
			},
		}
	}
</script>

<style>

</style>
