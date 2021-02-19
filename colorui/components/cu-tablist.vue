<template>
	<view>
		<view class="VerticalBox">
			<scroll-view class="VerticalNav nav" scroll-y scroll-with-animation :scroll-top="verticalNavTop" style="height:calc(100vh - 65upx)">
				<view class="cu-item" :class="index==tabCurr?'text-black cur':''" v-for="(item,index) in list" :key="index" @tap="TabSelect"
				 :data-id="index">
					{{item.title}}
				</view>
			</scroll-view>
			<scroll-view class="VerticalMain" scroll-y scroll-with-animation style="height:calc(100vh - 65upx)"
			 :scroll-into-view="'main-'+mainCur" @scroll="VerticalMain">
				<view class="padding-lr" v-for="(item,index) in list" :key="index" :id="'main-'+index">
					<view class="cu-bar">
						<view class="action">
							<text class="text-black"></text> {{item.title}}</view>
					</view>
					<view class="cu-list menu-avatar">
						<view class="cu-item" v-for="(item, index) in msgList" :key="index" @click="gotoTabDetails(item.id)">
							<!-- <view class="cu-avatar round lg" :style="'background-image:url('+ item.imgPath +')'"></view> -->
							<view>
								<image :src="item.imgPath" mode=""></image>
								<view>
									{{ item.title}}
								</view>
							</view>	
						</view>
						<!-- 解决flex布局问题 -->
						<view class="cu-item"></view>
						<view class="cu-item"></view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [
					{
						title: '为你推荐',
					},
					{
						title: '保养品牌区',
					},
					{
						title: '美容清洗',
					},
					{
						title: '常用配件',
					},
					{
						title: '常规保养',
					},
					{
						title: '美容清洗',
					},
					{
						title: '常规保养',
					},
					{
						title: '常用配件',
					},
					{
						title: '为你推荐',
					},
					{
						title: '保养品牌区',
					},
					{
						title: '保养品牌区',
					},
					{
						title: '保养品牌区',
					},	{
						title: '保养品牌区',
					}
				],
				msgList: [],
				tabCurr: 0,
				mainCur: 0,
				verticalNavTop: 0,
				load: true
			};
		},
		onLoad() {
			uni.showLoading({
				title: '加载中...',
				mask: true
			});
		},
		onReady() {
			uni.hideLoading()
		},
		methods: {
			// 请求数据
			getTabPage(){
		   // 	this.$api.getTabList().then((res)=>{
					// this.list = res.data.data
			  // });
				// this.$api.getMsgList().then((res)=>{
				// 	this.msgList = res.data.data
				// })
				this.msgList = 	[
					{
							imgPath: '../../static/image/1.png',
							title: '机油',
						},
						{
							imgPath: '../../static/image/2.png',
							title: '车载吸尘器',
						},
						{
							imgPath: '../../static/image/3.png',
							title: '玻璃水',
						},
						{
							imgPath: '../../static/image/2.png',
							title: '抱枕',
						},
						{
							imgPath: '../../static/image/1.png',
							title: '手机支架',
						},
						{
							imgPath: '../../static/image/2.png',
							title: '多功能手电',
						},
						{
							imgPath: '../../static/image/3.png',
							title: '耳机',
						},
				]
			},
			TabSelect(e) {
				this.tabCurr = e.currentTarget.dataset.id;
				this.mainCur = e.currentTarget.dataset.id;
				this.verticalNavTop = (e.currentTarget.dataset.id - 1) * 50
			},
			VerticalMain(e) {
				// #ifdef MP-ALIPAY
				   return false  //支付宝小程序暂时不支持双向联动 
				// #endif
				let that = this;
				let tabHeight = 0;
				if (this.load) {
					for (let i = 0; i < this.list.length; i++) {
					let view = uni.createSelectorQuery().select("#main-" + i);
					view.fields({
							size: true
						}, data => {
							this.list[i].top = tabHeight;
							tabHeight = tabHeight + data.height;
							this.list[i].bottom = tabHeight;
						}).exec();
					}
					this.load = false
				}
				let scrollTop = e.detail.scrollTop + 10;
				for (let i = 0; i < this.list.length; i++) {
					if (scrollTop > this.list[i].top && scrollTop < this.list[i].bottom) {
						this.verticalNavTop = (i) * 50
						this.tabCurr = i
						return false
					}
				}
			},
			gotoTabDetails(val){
				uni.navigateTo({
					url:'/pages/pagesA/details/details?id='+ val
				})
			}
		},
	}
</script>

<style lang="scss" scoped>
	.VerticalNav.nav {
		width: 280upx;
		white-space: initial;
		padding-bottom: 80rpx;
	}
  .padding-bt{
		padding-bottom: 30rpx;
	}
	.VerticalNav.nav .cu-item {
		width: 100%;
		text-align: center;
		background-color: #fff;
		margin: 0;
		border: none;
		position: relative;
		height: 100rpx;
		line-height: 100rpx;
	}
  .VerticalNav.nav .cu-item:first-child{
		border-radius: 0 15px 0 0;
	}
	.VerticalNav.nav .cu-item:last-child{
		border-radius: 0 0 15px 0;
	}
	.VerticalNav.nav .cu-item.cur {
		background-color: #F5F8FB;
		font-weight: 600;
	}

	.VerticalNav.nav .cu-item.cur::after {
		content: "";
		width: 8upx;
		height: 40upx;
		border-radius: 10upx;
		color: #FAA51F;
		position: absolute;
		background-color: currentColor;
		top: 0;
		bottom: 0;
		left: 0;
		margin: auto 0;
		margin-left: 20rpx;
	}

	.VerticalBox {
		display: flex;
	}
  .cu-list{
		text-align: center;
		box-shadow: 0px 6px 24px 0px rgba(212, 216, 225, 0.12);
		border-radius: 20px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		flex-wrap: wrap;
		.cu-item{
			width: calc(100% / 3);
			justify-content: center;
			align-items: center;
			padding: 30rpx 0;
			height: 180rpx;
		}
	   image{
			 width: 80rpx;
			 height: 80rpx;
		 }
		
	}
	.VerticalMain {
		background-color: #F5F8FB;
		padding-bottom: 80rpx;
	}
	.cu-list.menu-avatar>.cu-item:after, .cu-list.menu>.cu-item:after{
		border: none;
	}
	.cu-bar .action:first-child {
	 margin-left: 0rpx;
	 font-weight: 600;
	 font-size: 26rpx;
  }
	.text-aa{
		color: #FAA51F;
	}
</style>
