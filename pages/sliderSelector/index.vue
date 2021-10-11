<template>
	<view>
		<HevuNav title='滑块选择器' rightIcon='' @leftTag='leftTag'/>
		<view>
			<HevuSliderSelector/>
		</view>
	</view>
</template>

<script>
	import HevuNav from "@/componentsLayout/hevu-nav/components/hevu-nav/hevu-nav.vue"
	import HevuSliderSelector from "@/componentsLayout/hevu-slider-selector/components/hevu-slider-selector/hevu-slider-selector.vue"
	export default {
		data() {
			return {
				
			}
		},
		components: {
			HevuNav,
			HevuSliderSelector
		},
		methods: {
			leftTag(){
				uni.navigateBack()
			}
		}
	}
</script>

<style>

</style>
