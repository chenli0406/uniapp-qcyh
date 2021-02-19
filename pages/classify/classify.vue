<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="false">
			<block slot="backText">分类</block>
		</cu-custom>
	  <view style="margin-top: 40rpx;">
		<view style="width: 100%; overflow: hidden;">
			<cu-tablist ref="tablist"></cu-tablist>
		</view>
	</view>
	</view>
</template>

<script>
	import cuTablist from '../../colorui/components/cu-tablist.vue'
	export default {
		components: {
			cuTablist
		},
		data() {
			return {
				dataList: [],
				TabCur: 0,
				scrollLeft: 0,
				navList: [],
			};
		},
		onLoad() {
      this.getList();
		},
		methods: {
			// 获取数据
			getList() {
			 this.$refs.tablist.getTabPage();
			},
		}
	}
</script>

<style lang="scss">

</style>
