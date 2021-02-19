<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">商品(含服务)订单</block>
		</cu-custom>
		<van-sticky :offset-top="60">
		<scroll-view scroll-x class="nav" scroll-with-animation :scroll-left="scrollLeft">
			<view class="cu-item" :class="index==tabCur?'navActive':''" v-for="(item,index) in navList" :key="index" @tap="tabSelect"
			 :data-id="index">
				{{item.name}}
			</view>
		</scroll-view>
		</van-sticky>
		<view class="content">
			<view v-if="tabCur == '0'">
			<view class="cu-list sm-border menu bg-white" v-for="(item, index) in list" :key="index">
				<view style="text-align: right;font-weight: bold;">
					<text v-if="item.status == '1'" style="color:#F8A61F;">待付款</text>
					<text v-if="item.status == '2'" style="color:#F8A61F;">待发货</text>
					<text v-if="item.status == '3'" style="color:#29BF54;">已完成</text>
				</view>
				<view class="item" v-for="(key, i) in item.item" :key="i">
					<image :src="key.imgPath" mode=""></image>
					<view>
						<view style="font-size: 28rpx;">{{ key.title}}</view>
						<view class="price">
							<image src="../../../static/icon/1.png" mode=""></image>
							<text>{{ key.price }} 元</text>
						</view>
					</view>
				</view>
				<view class="list-box flex-z border-bottom">
					<text>预约时间</text>
					<text>{{ item.date }}</text>
				</view>
				<view class="list-box flex-z border-bottom">
					<text>订单编号</text>
					<text>{{ item.id }}</text>
				</view>
				<view class="list-box flex-z" @tap="gotoParticulars">
					<view>
						共 {{item.num}} 件  合计 {{item.totalPrices}} 元
					</view>
						<text class="cuIcon-right"></text>
				</view>
			</view>
			</view>
			<view v-if="tabCur == '1'">
				<text>13311</text>
			</view>
			<view v-if="tabCur == '2'">
				<text>11331</text>
			</view>
			<view v-if="tabCur == '3'">
				<text>111111</text>
			</view>
			<view v-if="tabCur == '4'">
				<text>1121</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tabCur: 0,
				scrollLeft: 0,
				navList: [{
						id: '1',
						name: '全部'
					},
					{
						id: '2',
						name: '待付款'
					},
					{
						id: '3',
						name: '待发货'
					},
					{
						id: '4',
						name: '待收货'
					},
					{
						id: '5',
						name: '待使用'
					},
				],
				list:[
					{
						item:[
							{
								imgPath: "../../../static/image/5.png",
								title: "汽车养护清洁 ×1",
								price: "188"
							},
							{
								imgPath: "../../../static/image/6.png",
								title: "一帆汽车美容特惠价机油...",
								price: "188"
							},
						],
						date: '2020-02-05 15:00',
						id: '15124846854454500',
						num: "2",
						totalPrices: '188',
						status: '1'
					},
					{
						item:[
							{
								imgPath: "../../../static/image/5.png",
								title: "汽车养护清洁 ×1",
								price: "188"
							},
						],
						date: '2020-02-05 15:00',
						id: '15124846854454500',
						num: "2",
						totalPrices: '188',
						status: '2'
					},
					{
						item:[
							{
								imgPath: "../../../static/image/5.png",
								title: "汽车养护清洁 ×1",
								price: "188"
							},
						],
						date: '2020-02-05 15:00',
						id: '15124846854454500',
						num: "2",
						totalPrices: '188',
						status: '3'
					}
				]
			};
		},
		methods: {
			tabSelect(e) {
				this.tabCur = e.currentTarget.dataset.id;
				this.scrollLeft = (e.currentTarget.dataset.id - 1) * 60;
			},
			// 详情
			gotoParticulars(){
				uni.navigateTo({
					url: '/pages/pagesB/afterSaleParticulars/afterSaleParticulars'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.nav {
    padding-top: 20rpx;
		padding-bottom: 20rpx;
		background-color: #F5F8FB;
		.cu-item {
			width: 20%;
			text-align: center;
			height: 60rpx;
			line-height: 60rpx;
		}

		.navActive {
			background: #F8A61F;
			border-radius: 30rpx;
			color: #fff;
		}
	}
	.cu-list {
				border-radius: 20px;
			  padding: 20rpx;
				.item{
					font-weight: bold;
					display: flex;
					align-items: center;
					margin: 20rpx;
					image {
						width: 160rpx;
						height: 120rpx;
						margin-right: 40rpx;
					}
					.price{
						display: flex;
						align-items: center;
						padding: 15rpx 0;
						image {
							width: 30rpx;
							height: 30rpx;
							margin-right: 20rpx;
						}
					}
				}
				.list-box{
					padding: 20rpx;
				}
	 }
</style>
