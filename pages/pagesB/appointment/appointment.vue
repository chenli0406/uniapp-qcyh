<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText" class="back-box">我的预约</block>
		</cu-custom>
		<view class="content">
			<view class="cu-list sm-border menu bg-white" v-for="(item, index) in list" :key="index">
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
	</view>
</template>

<script>
	export default {
		data() {
			return {
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
								title: "汽车养护清洁 ×1",
								price: "188"
							}
						],
						date: '2020-02-05 15:00',
						id: '15124846854454500',
						num: "2",
						totalPrices: '188',
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
					}
				]
			};
		},
		methods:{
			// 详情
			gotoParticulars(){
				uni.navigateTo({
					url: '/pages/pagesB/orderParticulars/orderParticulars'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
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
