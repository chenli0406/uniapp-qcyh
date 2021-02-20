<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">帮助中心</block>
		</cu-custom>
		<view class="content">
			<view class="head bg-white mar-30">
				<view class="flex-z pad-10" v-for="(item, index) in list" :key="index" @click="gotoParticulars(item.id)" >
					<view class="ellipsis-d">{{ item.title }}</view>
					<text class="cuIcon-right"></text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [{
					id:'1',
						title: 'XX问题',
					},
					{
						id:'1',
						title: 'XX问题',
					},
					{
						id:'1',
						title: 'XX问题XX问题XX问题XX问题XX问题XX问',
					},
					{
						id:'1',
						title: 'XX问题',
					}, 
					{
						id:'1',
						title: 'XX问题',
					},
					{
						id:'1',
						title: 'XX问题',
					},
					{
						id:'1',
						title: 'XX问题',
					}
				]
			};
		},
		onLoad() {},
		methods: {
			gotoParticulars(id) {
				uni.navigateTo({
					url: `/pages/pagesB/helpCenterParticulars/helpCenterParticulars?id=${id}`
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
</style>
