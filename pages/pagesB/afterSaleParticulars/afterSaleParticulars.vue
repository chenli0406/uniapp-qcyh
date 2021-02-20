<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">订单详情页</block>
		</cu-custom>
		<view class="content">
			<view class="head bg-white" v-if="state == '3'">
				<view class="head_bold">
					<image src="../../../static/icon/2.png" mode=""></image>
					<text class="text-z">待审批</text>
				</view>
				<view style="text-align: center;padding: 10rpx;">卖家将在3天内处理该申请，超时将自动同意</view>
			</view>
			<view class="head bg-white" v-if="state == '2'">
				<view class="head_bold">
					<image src="../../../static/icon/2.png" mode=""></image>
					<text class="text-z">待退货</text>
				</view>
				<view style="text-align: center;padding: 10rpx;">您需要在3天间内退货，超时将取消</view>
			</view>
			<view class="head bg-white" v-if="state == '4'">
				<view class="head_bold">
					<image src="../../../static/icon/2.png" mode=""></image>
					<text class="text-z">未通过</text>
				</view>
				<view style="text-align: center;padding: 10rpx;">您的XX信息填写错误，请重新填写</view>
			</view>
			<view class="head bg-white" v-if="state == '1'">
				<view class="head_bold">
					<image src="../../../static/icon/3.png" mode=""></image>
					<text class="text-z">已退货</text>
				</view>
				<view style="text-align: center;padding: 10rpx;">等待卖家确认</view>
			</view>
			<view class="head bg-white mar-30">
				<view class="flex-z border-bottom pad-20">
					<text class="text-black">售后类型</text>
					<text>仅退款</text>
				</view>
				<view class="flex-z pad-20">
					<text class="text-black">退款金额</text>
					<view>¥ <text class="text-black">300</text> </view>
				</view>
			</view>
			<view class="bold">退款信息</view>
			<view class="head bg-white mar-30">
				<view class="refund flex-c pad-b-20">
					<image src="../../../static/image/5.png" mode=""></image>
					<view>
						<view style="font-size: 28rpx;" class="text-black">一帆汽车美容(环球店)</view>
						<view style="color: #777;font-size: 22rpx; margin: 14rpx 0;">汽车养护清洁 ×1 </view>
					</view>
				</view>
				<view class="refund flex-c pad-b-20">
					<image src="../../../static/image/5.png" mode=""></image>
					<view>
						<view style="font-size: 28rpx;" class="text-black">一帆汽车美容(环球店)</view>
						<view style="color: #777;font-size: 22rpx; margin: 8rpx 0;">汽车养护清洁 ×1 </view>
						<view class="price">
							<image src="../../../static/icon/1.png" mode=""></image>
							<text>300 元</text>
						</view>
					</view>
				</view>
			</view>
			<view class="bold">退款凭证(最多3张)</view>
			<view class="img-box pad-20">
				<image src="../../../static/image/7.png" mode=""></image>
				<image src="../../../static/image/7.png" mode=""></image>
				<image src="../../../static/image/7.png" mode=""></image>
				<image style="height: 0;" src="" mode=""></image>
			</view>
			<view class="head bg-white mar-30">
				<view class="flex-z pad-10">
					<text class="text-black">订单编号</text>
					<text>151245748541212</text>
				</view>
				<view class="flex-z pad-10">
					<text class="text-black">退款原因</text>
					<text>多拍/拍错等</text>
				</view>
				<view class="flex-z pad-10">
					<text class="text-black">退款说明</text>
					<text>商品有瑕疵</text>
				</view>
				<view class="flex-z pad-10">
					<text class="text-black">核销时间</text>
					<text>2020-02-03 15:00</text>
				</view>
				<view class="flex-z pad-10">
					<text class="text-black">申请时间</text>
					<text>2020-02-03 15:00</text>
				</view>
				<view class="flex-z pad-10">
					<text class="text-black">售后编号</text>
					<text>4546512313848131</text>
				</view>
			</view>
			<view class="bold">退货地址</view>
			<view class="head bg-white mar-30 info" style="margin-bottom: 120rpx;">
				<view class="flex-c pad-10">
					<image src="../../../static/icon/my.png" mode=""></image>
					<text class="text-black">李大宝</text>
				</view>
				<view class="flex-c pad-10">
					<image src="../../../static/icon/phone.png" mode=""></image>
					<text class="text-black">15282094560</text>
				</view>
				<view class="flex-c pad-10">
					<image src="../../../static/icon/address.png" mode=""></image>
					<text class="text-black">成都市武侯区锦悦西路环球中心</text>
				</view>
			</view>
		</view>
		<view class="flex-direction btn1">
			<button v-if="state == '2'" class="cu-btn bg-themeColor lg" @tap="cancelApply">取消申请</button>
			<button v-if="state == '3'" class="cu-btn bg-themeColor lg" @tap="show = true">立即退货</button>
			<button v-if="state == '1'" class="cu-btn bg-themeColor lg" @tap="gotoContactService">联系客服</button>
		</view>
		<van-action-sheet round :show="show" title="立即退货" bind:close="onHide">
			<view class="from-box">
				<view class="cu-form-group">
					<input placeholder="请输入物流公司名称" v-model="from.name" name="input"></input>
				</view>
				<view class="cu-form-group">
					<input placeholder="请输入物流单号" v-model="from.num" name="input"></input>
				</view>
				<view class="flex-direction btn">
					<button class="cu-btn bg-themeColor lg" @tap="onSubmit">确认</button>
				</view>
			</view>
		</van-action-sheet>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				state: '1',
				show: false,
				from:{
					name: '',
					num: ''
				}
			};
		},
		methods: {
			cancelApply() {
				uni.navigateTo({
					url: "/pages/pagesB/resultPage/resultPage?title=取消申请"
				})
			},
			onHide() {
				this.show = false;
				this.from={
					name: '',
					num: ''
				}
			},
			onSubmit(){
				if(this.from.name  == ''){
					uni.showToast({
					    title: '物流公司名称不能为空',
							icon:'none',
					});
					return;
				}
				if(this.from.num  == ''){
					uni.showToast({
					    title: '物流单号不能为空',
							icon:'none',
					});
					return;
				}
				// this.show = false;
				return false;
			},
			// 联系客服
			gotoContactService(){
				uni.navigateTo({
					url: '/pages/pagesB/contactService/contactService'
				})
			}
		}

	}
</script>

<style lang="scss" scoped>
	.head {
		padding: 20rpx 30rpx;

		.head_bold {
			display: flex;
			align-items: center;
			justify-content: center;
			image {
				width: 50rpx;
				height: 50rpx;
				margin-left: 20rpx;
				margin-top: 16rpx;
			}
		}

		.text-black {
			font-weight: 600;
		}
	}

	.refund {
		image {
			width: 160rpx;
			height: 120rpx;
			margin-right: 40rpx;
		}
	}

	.img-box {
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;

		image {
			width: 30%;
			height: 140rpx;
			border-radius: 10rpx;
		}
	}

	.btn1 {
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

	.price {
		display: flex;
		align-items: center;

		image {
			width: 30rpx;
			height: 30rpx;
			margin-right: 20rpx;
		}
	}

	.info {
		image {
			width: 36rpx;
			height: 36rpx;
			margin-right: 40rpx;
		}
	}

	.from-box {
		padding: 20rpx 30rpx;
		.btn {
			width: 100%;
			bottom: 0;
			text-align: center;
			.cu-btn {
				width: 90%;
				margin: 30rpx 0;
				border-radius: 40rpx;
			}
		}
		.cu-form-group{
			background: #F5F8FB;
			border-radius: 44rpx;
			margin: 30rpx 0;
			padding: 20rpx 40rpx;
			min-height: auto;
			input{
				height: auto;
			}
		}
	}
</style>
