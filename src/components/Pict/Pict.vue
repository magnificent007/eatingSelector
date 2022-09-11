<template>
	<view class="content">
		<image class="card" mode="aspectFill" src="@/static/photos/1.jpeg"></image>
		<image class="card" mode="aspectFill" src="@/static/photos/2.jpeg"></image>
		<image class="card" mode="aspectFill" src="@/static/photos/3.jpeg"></image>
		<image class="card" mode="aspectFill" src="@/static/photos/24.jpg"></image>
		<image class="card" mode="aspectFill" src="@/static/photos/5.jpeg"></image>
		<image class="card" mode="aspectFill" src="@/static/photos/25.png"></image>
	</view>
</template>

<script>
	export default {
		name:"Pict",
		data() {
			return {
				
			};
		},
		mounted() {
			uni.getSystemInfo({
				success:function(res){
					console.log(res)
				}
			})
		}
	}
</script>

<style scoped>
	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}
	
	.content{
		width: 100vw;
		padding: 30rpx;
		display: flex;
		align-items: flex-start;
		justify-content: space-around;
		flex-wrap: wrap;
	}
	
	.card{
		width: 40vw;
		margin-bottom: 30rpx;
		border-radius: 30rpx;
	}
</style>
