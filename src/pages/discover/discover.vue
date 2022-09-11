<template>
	<view>
		<Pict></Pict>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		},
		onLoad() {
			
		},
		onPullDownRefresh() {
			let timer = null
			clearTimeout(timer)
			console.log('trigger PullDownRefresh')
			setTimeout(() =>{
				uni.stopPullDownRefresh()
				uni.showToast({
					title: '刷新成功',
					icon: 'success'
				})
			}, 1500)
		},
		onReachBottom() {
			console.log('trigger ReachBottom')
		}
	}
</script>

<style scoped>

</style>
