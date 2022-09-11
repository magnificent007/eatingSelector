<template>
  <view class="u-page">
	<view id="title">{{title}}</view>
	<view id="place">{{place}}</view>
    <editor
		id="editor"
		placeholder='请输入淦饭地点(地点间以空格分离)'
		showImgToolbar
		@ready="onEditorReady"
		@blur="getEditorCotext">
	</editor>
	<view id="btnGrop">
		<button type="primary" size="mini" @click="select">开始</button>
		<button type="primary" size="mini" @click="stop">暂停</button>
		<button type="warn" size="mini" @click="clear">撤销</button>
	</view>
  </view>
</template>

<script>
	import {ref, reactive} from 'vue'
	export default {
	  setup() {
		  let title = ref('淦饭人淦饭魂')
		  let place = ref('暂无地点')
		  
		  let editorCtx = reactive({})
		  
		  let timer
		  let placeArr = []
		  
		  function onEditorReady() {
			  uni.createSelectorQuery().select('#editor').context((res) => {
				  editorCtx = res.context
				  if(uni.getStorageSync('placeArr'))
					editorCtx.setContents({
						html: `<p>${uni.getStorageSync('placeArr').toString()}</p>`
					})
					placeArr = uni.getStorageSync('placeArr')
			  }).exec()
		  }
		  
		  function getEditorCotext() {
			  editorCtx.getContents({
				  success(res) {
					  if(res.text.split('\n')[0] === ''){
						  place.value = '暂无地点'
						  uni.removeStorageSync('placeArr');
						  return
					  }
					  placeArr = res.text.split('\n')[0].split(' ')
					  uni.setStorageSync('placeArr', placeArr)
				  }
			  })
		  }
		  
		  function clear() {
			  editorCtx.clear({
			  	success(res){
					uni.removeStorageSync('placeArr');
					place.value = '暂无地点'
					placeArr = []
					console.log(res)
				}
			  })
		  }
		  
		  function select() {
			  let len = placeArr.length
			  if(!len)
				return
			  let i = 0
			  timer = setInterval(() => {
				  if(i > len - 1)
					i = 0
				  place.value = placeArr[i]
				  i++
			  }, 80)
		  }
		  
		  function stop() {
			  clearInterval(timer)
		  }
		  
		  return {
			  title,
			  place,
			  
			  onEditorReady,
			  getEditorCotext,
			  clear,
			  select,
			  stop
		  }
	  },
	  onLoad() {}
	}
</script>

<style scoped>
	.u-page{
		padding: 40rpx;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center
	}
	
	#title{
		margin: 40rpx 0 0 0;
		/* font-family: 宋体; */
		font-size: 24px;
		font-weight: bold;
	}
	
	#place{
		margin: 40rpx 0 0 0;
		font-size: 20px;
	}
	
	#editor{
		margin: 40rpx 0 0 0;
		width: 100%;
		border: 1px solid #b3b3b3;
	}
	
	#btnGrop{
		margin: 40rpx 0 0 0;
		width: 100%;
		display: flex;
	}
</style>
