<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">{{ title }}</block>
		</cu-custom>
		<view class="content">
			<view class="head bg-white mar-30">
				<view class="pad-10 box">
					<image src="../../../static/image/success.png" mode=""></image>
					<view class="text-black mar-30">取消申请成功</view>
					<view class="head_btn">
						<button class="cu-btn bg-themeColor round lg" @tap="goHome">返回首页</button>
					</view>	
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
			};
		},
		onLoad(option) {
			this.title = option.title
		},
		methods:{
			goHome(){
				uni.navigateTo({
					url: "/pages/index/index"
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
.box{
	text-align: center;
	image{
		width: 80rpx;
		height: 80rpx;
	}
	.text-black{
		font-weight: 600;
	}
}
</style>
