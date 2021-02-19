<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="false">
			<block slot="backText">我的</block>
		</cu-custom>
		<view class="content">
			<view class="head bg-white">
				<view class="avatar-box">
					<view class="cu-avatar xl round" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big99008.jpg);"></view>
				</view>
				<view class="head_bold" style="text-align: center;margin-top: 40rpx;">何花落去</view>
				<view class="head_menu">
					<view>
						<view class="head_bold">9</view>
						<text>洗车券</text>
					</view>
					<view>
						<view class="head_bold">7</view>
						<text>购物车</text>
					</view>
					<view @tap="gotoAppointment">
						<view class="head_bold">-</view>
						<text>我的预约</text>
					</view>
					<view>
						<view class="head_bold">779</view>
						<text>我的钱包</text>
					</view>
				</view>
			</view>
			<view class="cu-list sm-border card-menu menu bg-white ">
				<view class="cu-item arrow" v-for="(item, index) in menuList" :key="index" @tap="gotoListUrl(item.url)">
					<button class="cu-btn content" @tap="setShowModal">
						<image :src="item.imgPath"></image>
						<text class="text-black"> {{ item.name }}</text>
					</button>
				</view>
			</view>
			<view class="list">
				<view class="list-item" v-for="(item, index) in list" :key="index" @tap="gotoListUrl(item.url)">
					<image :src="item.imgPath"></image>
					<view>{{ item.name }}</view>
				</view>
				<view class="list-item"></view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				menuList: [{
						name: '商品订单',
						imgPath: '../../static/icon/menu-1.png',
						url:'/pages/pagesB/order/order'
					},
					{
						name: '服务订单',
						imgPath: '../../static/icon/menu-2.png'
					},
					{
						name: '商品（含服务）订单',
						imgPath: '../../static/icon/menu-3.png',
						url: '/pages/pagesB/serveOrderList/serveOrderList'
					},
					{
						name: '售后订单',
						imgPath: '../../static/icon/menu-4.png',
						url: '/pages/pagesB/afterSaleOrderList/afterSaleOrderList'
					},
				],
				list: [{
						name: '我的佣金',
						imgPath: '../../static/icon/list-1.png',
						url: '/pages/pagesB/commission/commission'
					},
					{
						name: '我的推广',
						imgPath: '../../static/icon/list-2.png',
						url: '/pages/pagesB/promotion/promotion'
					},
					{
						name: '爱车档案',
						imgPath: '../../static/icon/list-3.png',
						url: '/pages/pagesB/promotion/promotion'
					},
					{
						name: '联系客服',
						imgPath: '../../static/icon/list-4.png',
						url: '/pages/pagesB/promotion/promotion'
					},
					{
						name: '关于我们',
						imgPath: '../../static/icon/list-5.png',
						url: '/pages/pagesB/promotion/promotion'
					},
					{
						name: '帮助中心',
						imgPath: '../../static/icon/list-6.png',
						url: '/pages/pagesB/promotion/promotion'
					},
					{
						name: '意见反馈',
						imgPath: '../../static/icon/list-7.png',
						url: '/pages/pagesB/promotion/promotion'
					},
				]
			}
		},
		methods: {
     gotoListUrl(url){
			 uni.navigateTo({
			 	url: url
			 })
		 },
		 gotoAppointment(){
			 uni.navigateTo({
			 	url: '/pages/pagesB/appointment/appointment'
			 })
		 }
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		.head {
			border-radius: 20px;
			margin: 60rpx 0 20rpx 0;
			padding: 30rpx 40rpx;
			position: relative;

			.cu-avatar.xl {
				border: 2px solid #FAA51F;
				width: 138rpx;
				height: 138rpx;
			}

			.head_menu {
				display: flex;
				justify-content: space-between;
				align-items: center;
				text-align: center;
				padding: 15rpx 0;

			}

			.avatar-box {
				position: absolute;
				left: 50%;
				margin-left: -69rpx;
				margin-top: -100rpx;
			}

			.head_bold {
				font-weight: 600;
				color: #000;
				font-size: 30rpx;
				padding: 6rpx 0;
			}
		}

		.menu {
			border-radius: 20px;
			margin: 20rpx 0;
			padding:20rpx 30rpx;
		}

		.cu-list.menu>.cu-item {
			padding: 0;
		}

		.cu-list.menu-avatar>.cu-item:after,
		.cu-list.menu>.cu-item:after {
			border-bottom: none;
		}

		.cu-list.menu>.cu-item .content>image {
			width: 40rpx;
			height: 38rpx;
			margin-right: 25rpx;
		}

		.list {
			display: flex;
			flex-wrap: wrap;
			align-items: center;
			justify-content: space-between;
      .list-item{
				width: 25%;
				padding: 15rpx 0;
				color: #777;
				text-align: center;
				image{
					width: 38rpx;
					height: 38rpx;
				}
			}
		}
	}
</style>
