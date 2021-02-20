<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">联系客服</block>
		</cu-custom>
		<view class="content">
			<view class="head bg-white mar-30">
				<view class="flex-z pad-20">
					<view class="flex-c">
						<view class="text-black">电话号码 &nbsp;</view>
						<view class="text-black">15282041597</view>
					</view>
					<view>
						<button class="cu-btn round"  @tap="callPhone">拨打</button>
					</view>
				</view>
				<view class="flex-z pad-20">
					<view class="flex-c">
						<view class="text-black">电话号码</view>
						<view class="text-black">15282041597</view>
					</view>
					<view>
						<button class="cu-btn round"  @tap="copy('111')">复制</button>
					</view>
				</view>
				<view class="flex-z pad-20">
					<view class="flex-c">
						<view class="text-black">电话号码</view>
						<view class="text-black">15282041597</view>
					</view>
					<view>
						<button class="cu-btn round"  @tap="copy('22')">复制</button>
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
				
			};
		},
		onLoad(){
		},
		methods:{
			callPhone(){
				uni.makePhoneCall({
				    phoneNumber: '123466'
				});
			},
			copy(val){
				uni.setClipboardData({
				    data: val,
				    success: function () {
				        console.log('success');
				    }
				});
			}
		}
	}
</script>

<style lang="scss">
.text-black{
	font-weight: 600;
	margin-right: 20rpx;
}
.cu-btn{
	padding: 15rpx 40rpx;
	color: #fff;
	background-color: #29BF54!important;
}
</style>
