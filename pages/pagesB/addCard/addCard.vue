<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">{{ title }}</block>
		</cu-custom>
		<view class="content">
			<view class="from-box">
				<view class="mar-30">
					<text class="text-black">车辆品牌</text>
					<view class="cu-form-group">
						<input placeholder="请输入车辆品牌" v-model="from.name" name="input"></input>
					</view>
				</view>
				<view class="mar-30">
					<text class="text-black">车辆款型</text>
					<view class="cu-form-group">
						<input placeholder="请输入车辆款型" v-model="from.type" name="input"></input>
					</view>
				</view>
				<view class="mar-30">
					<text class="text-black">车牌号</text>
					<view class="cu-form-group">
						<input placeholder="请输入车牌号" v-model="from.number" name="input"></input>
					</view>
				</view>
				<view class="mar-30">
					<view class="cu-form-group flex-z">
						<text class="text-black">设为默认车辆</text>
						<van-switch size="20px" @change="onChange" :checked="checked" active-color="#29BF54" inactive-color="#fff" />
					</view>
				</view>
				<view class="mar-30" @tap="del">
					<text class="text-z">删除车辆信息</text>
				</view>
			</view>
		</view>
		<view class="flex-direction btn">
			<button class="cu-btn bg-themeColor lg" @tap="onSubmit">确定</button>
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
				title: '',
				type: undefined,
				checked: true,
			};
		},
		onLoad(options) {
			this.title = options.title;
			this.type = options.type;
		},
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
			onChange(){
				this.checked = !this.checked;
			},
			del(){}
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
	}
</style>
