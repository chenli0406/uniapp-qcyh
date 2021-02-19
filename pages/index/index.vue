<template>
	<view class="container">
	  <cu-custom bgColor="nav-bg" :isBack="true" :isShow="false">
	      <block slot="backText">汽车保养服务站</block>
	  </cu-custom>
	</view>
</template>

<script>

	export default {
		data() {
			return {
			
			}
		},
		onLoad() {
			uni.showLoading({
				title: '加载中...',
				mask: true
			});
		},
		onReady(){
			uni.hideLoading()
		},
		// 监听推荐组件触底（在组件中这个不执行）
		onReachBottom(){
	
		},
		methods: {
		}
	}
</script>

<style lang="scss">
</style>
