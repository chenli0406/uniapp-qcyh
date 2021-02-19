<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText" class="back-box">
				我的佣金
				<view class="warning-box" @tap.stop="showDialog">
					<image src="../../../static/icon/warning.png" mode=""></image>
				</view>
			</block>
		</cu-custom>
		<view class="content">
			<view class="head bg-white">
				<view>
					<text class="text-black">¥</text>
					<text class="head_bold text-black">209</text>
					<view style="padding: 20rpx 0;">
						最低提现额度¥300
					</view>
				</view>
				<view class="head_btn">
					<button class="cu-btn line round lg lines">立即提现</button>
				</view>
			</view>
			<view class="list">
				<van-sticky :offset-top="60">
					<view class="tab_wrap">
						<button class="cu-btn round lg" :class="{ tab_active: tab == 1 }" @tap="tabIndex('1')">佣金记录</button>
						<button class="cu-btn round lg" :class="{ tab_active: tab == 2 }" @tap="tabIndex('2')">提现记录</button>
					</view>
				</van-sticky>
				<view class="cu-list sm-border menu bg-white" style="margin-bottom: 120rpx;">
					<view v-if="tab == 1">
						<view class="cu-item arrow" v-for="(item, index) in list" :key="index">
							<button class="cu-btn">
								<view style="text-align: left;">
									<view class="cu-avatar lg round" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big99008.jpg);"></view>
									<text class="text-black"> {{ item.title }}</text>
									<view class="date">
										{{ item.date }}
									</view>
								</view>
							<view>
								<text> 佣金 ¥ {{ item.price }}</text>
								<text class="cuIcon-right"></text>
							</view>
							</button>
						</view>
					</view>
					<view v-if="tab == 2">
						<view class="cu-item arrow" v-for="(item, index) in list1" :key="index">
							<button class="cu-btn">
								<view style="text-align: left;">
									<text class="text-black"> {{ item.title }}</text>
									<view class="date">
										{{ item.date }} 申请提现
									</view>
								</view>
								<view>
									<text> ￥ {{ item.price }}</text>
									<text class="cuIcon-right"></text>
								</view>
							</button>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="flex-direction btn">
			<button class="cu-btn bg-themeColor lg">银行卡管理</button>
		</view>
		<!-- 对话框 -->
		<van-dialog use-slot title="我的佣金规则说明" :show="show" width="70%" class="dialog" confirm-button-color="'#fff'"
		 confirmButtonText="关闭" @confirm="confirm">
			<view class="dialog-content">
				<view class="dialog-icon">
					<image src="../../../static/image/dialog.png" mode=""></image>
				</view>
				Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean euismod bibendum laoreet. Proin gravida dolor sit
				amet lacus accumsan et viverra justo commodo. Proin sodales pulvinar sic tempor. Sociis natoque penatibus et magnis
				dis parturient montes, nascetur ridiculus mus. Nam fermentum, nulla luctus pharetra vulputate, felis tellus mollis
				orci, sed rhoncus pronin sapien nunc accuan eget.
			</view>
		</van-dialog>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				show: false,
				tab: 1,
				list: [
					{
						title: '待结算',
						date: '2020-01-01',
						price: '200'
					},
					{
						title: '待结算',
						date: '2020-01-01',
						price: '200'
					},
					{
						title: '待结算',
						date: '2020-01-01',
						price: '200'
					},
					{
						title: '待结算',
						date: '2020-01-01',
						price: '200'
					},
					{
						title: '待结算',
						date: '2020-01-01',
						price: '200'
					},
					{
						title: '待结算',
						date: '2020-01-01',
						price: '200'
					},
					{
						title: '待结算',
						date: '2020-01-01',
						price: '200'
					},
				],
				list1: [{
						title: '昵称',
						date: '2020-01-01',
						price: '200',
					},
					{
						title: '昵称',
						date: '2020-01-01',
						price: '200'
					},
					{
						title: '昵称',
						date: '2020-01-01',
						price: '200'
					},
					{
						title: '昵称',
						date: '2020-01-01',
						price: '200'
					}
				]
			};
		},
		methods: {
			showDialog() {
				this.show = true;
			},
			confirm() {
				this.show = false;
			},
			tabIndex(val) {
				this.tab = val;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.back-box {
		display: flex;
		align-items: center;

		.warning-box {
			display: inline;
			margin: 0 15rpx;

			image {
				width: 30rpx;
				height: 30rpx;
				margin-top: 10rpx;
			}
		}
	}

	.dialog {
		position: relative;

		.dialog-content {
			padding: 20rpx 30rpx;
			font-size: 24rpx;
			text-align: justify;
		}

		.dialog-icon {
			position: absolute;
			top: -50rpx;
			z-index: 9999999;
			left: 50%;
			margin-left: -60rpx;

			image {
				width: 120rpx;
				height: 120rpx;
			}
		}
	}

	.head {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 30rpx 50rpx;
		margin: 20rpx 0;

		.head_bold {
			font-size: 40rpx;
		}
	}

	.list {
		border-radius: 20px;
		padding: 10rpx 0;
		margin: 20rpx 0;
		.tab_wrap {
			display: flex;
			justify-content: space-between;
			align-items: center;
			padding: 20rpx 50rpx;
      background-color: #F5F8FB;
			.tab_active {
				background-color: #F8A61F;
				color: #fff;
			}
		}

		.cu-list {
			border-radius: 20px;
			padding: 10rpx 0 20rpx 0;

			.cu-item {
				padding: 20rpx;
				
				.cu-avatar {
					width: 60rpx;
					height: 60rpx;
					margin-right: 26rpx;
				}

				.date {
					color: #666;
					font-size: 22rpx;
					padding: 12rpx 0;
				}
				.text-black{
					font-weight: 600;
				}
			}

			.cu-btn {
				width: 100%;
				background-color: #fff;
				justify-content: space-between;
        align-items: center;
				// border-bottom: 1px solid #eee;
			}
		}
	}
	.btn{
		width: 100%;
		position: fixed;
		bottom: 0;
		 background-color: #F5F8FB;
		 text-align: center;
		 .cu-btn{
			 width: 90%;
			 margin: 30rpx 0;
			 border-radius: 40rpx;
		 }
	}
</style>
