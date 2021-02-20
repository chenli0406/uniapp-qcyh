<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">问题详情</block>
		</cu-custom>
		<view class="content">
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		onLoad(option){
			console.log(option)
	  }
		
	}
</script>

<style lang="scss" scoped>

</style>
