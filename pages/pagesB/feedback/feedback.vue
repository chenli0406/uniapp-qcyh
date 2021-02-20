<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">意见反馈</block>
		</cu-custom>
		<view class="content">
			<view class="from-box">
				<view class="cu-form-group flex-z mar-30">
					<text class="text-black">车辆品牌</text>
					<input placeholder="请输入车辆品牌" v-model="from.name" name="input"></input>
				</view>
				<view class="cu-form-group flex-z mar-30" style="padding: 0 40rpx;">
					
					<textarea maxlength="-1" v-model="from.number" :maxlength="200" placeholder="请输入反馈内容(文字不超过200字)"></textarea>
				</view>
				<view class="cu-form-group flex-z mar-30">
						<text class="text-black">联系方式</text>
						<input placeholder="邮箱/手机号" v-model="from.number" name="input"></input>
				</view>
			</view>
		</view>
		<view class="flex-direction btn">
			<button class="cu-btn bg-themeColor lg" @tap="onSubmit">提交</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				from: {
					name: '',
					type: '',
					number: '',
				},
			};
		},
		onLoad(options) {},
		methods: {
			onSubmit() {
				if (this.from.name == '') {
					uni.showToast({
						title: '车辆品牌不能为空',
						icon: 'none',
					});
					return;
				}
				if (this.from.type == '') {
					uni.showToast({
						title: '车辆款型不能为空',
						icon: 'none',
					});
					return;
				}
				if (this.from.number == '') {
					uni.showToast({
						title: '车牌号不能为空',
						icon: 'none',
					});
					return;
				}
				return false;
			},
		}
	}
</script>

<style lang="scss" scoped>
	.text-black {
		font-weight: 600;
	}

	.btn {
		width: 100%;
		position: fixed;
		bottom: 0;
		background-color: #F5F8FB;
		text-align: center;

		.cu-btn {
			width: 90%;
			margin: 30rpx 0;
			border-radius: 40rpx;
		}
	}

	.cu-form-group {
		margin-top: 30rpx;
		border-radius: 50rpx;
		padding: 20rpx 40rpx;
		min-height: auto;
		input{
			text-align: right;
		}
	}
</style>
