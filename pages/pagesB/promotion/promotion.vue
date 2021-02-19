<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">我的推广</block>
		</cu-custom>
		<view class="content">
			<view class="head bg-white">
				<view class="head_bold text-black" style="text-align: center;">推广二维码</view>
				<view style="text-align: center;padding: 20rpx;">快去分享二维码增加您的团队成员吧~</view>
				<view class="head_box">
					<image :src="erweimaPath" mode=""></image>
				</view>
				<view class="head_btn">
					<button class="cu-btn bg-themeColor round lg" @tap="savePoster">复制二维码</button>
				</view>	
			</view>
			<view class="bold">我的团队</view>
		 <view class="cu-list sm-border menu bg-white ">
			<view class="cu-item" v-for="(item, index) in list" :key="index">
				<button class="cu-btn">
					<view>
						<view class="cu-avatar lg round" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big99008.jpg);"></view>
						<text class="text-black"> {{ item.name }}</text>
					</view>
					<text class="date"> 绑定时间 {{ item.date }}</text>
				</button>
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
						name: '李大宝',
						imgPath: '../../../static/image/4.png',
						date: '2020-01-01'
					},
					{
						name: '李大宝',
						imgPath: '../../../static/image/4.png',
						date: '2020-01-01'
					},
					{
						name: '李大宝',
						imgPath: '../../../static/image/4.png',
						date: '2020-01-01'
					},{
						name: '李大宝',
						imgPath: '../../../static/image/4.png',
						date: '2020-01-01'
					}
				],
				erweimaPath: '../../../static/image/erweima.png',
			};
		},
		onLoad() {
		},
		methods: {
		  // 复制
			savePoster() {
				uni.getSetting({ //获取用户的当前设置
					success: (res) => {
						if (res.authSetting['scope.writePhotosAlbum']) { //验证用户是否授权可以访问相册
							this.saveImageToPhotosAlbum();
						} else {
							uni.authorize({ //如果没有授权，向用户发起请求
								scope: 'scope.writePhotosAlbum',
								success: () => {
									this.saveImageToPhotosAlbum();
								},
								fail: () => {
									uni.showToast({
										title: "请打开保存相册权限，再点击保存图片",
										icon: "none",
										duration: 3000
									});
									setTimeout(() => {
										uni.openSetting({ //调起客户端小程序设置界面,让用户开启访问相册
											success: (res2) => {
												// console.log(res2.authSetting)
											}
										});
									}, 3000);
								}
							})
						}
					}
				})
			},
			saveImageToPhotosAlbum() {
				// let base64 = this.src2.replace(/^data:image\/\w+;base64,/, ""); //去掉data:image/png;base64,
				let filePath = this.erweimaPath;
				uni.showLoading({
					title: '加载中',
					mask: true
				})
				uni.getFileSystemManager().writeFile({
					filePath: filePath, //创建一个临时文件名
					// data: base64, //写入的文本或二进制数据
					// encoding: 'base64', //写入当前文件的字符编码
					success: res => {
						uni.saveImageToPhotosAlbum({
							filePath: filePath,
							success: function(res2) {
								uni.hideLoading();
								uni.showToast({
									title: '保存成功',
									icon: "none",
									duration: 5000
								})
							},
							fail: function(err) {
								uni.hideLoading();
								// console.log(err.errMsg);
							}
						})
					},
					fail: err => {
						uni.hideLoading();
						//console.log(err)
					}
				})
			},
			copy(){
				uni.saveImageToPhotosAlbum({
				    filePath: this.erweimaPath,
				    success: function () {
				        console.log('save success');
							uni.showToast({
								icon: "none",
								title: "保存成功",
								duration: 2000
							});
				    },
						fail:function () {
				        console.log('1');
								uni.showToast({
									icon: "none",
									title: "保存失败",
									duration: 2000
								});
				    },
				});
			}

		}
	}
</script>

<style lang="scss" scoped>
 .head{
	 .head_box{
		 text-align: center;
		 padding: 10rpx 0;
		 image{
			 width: 240rpx;
			 height: 240rpx;
		 }
	 }
	 .head_btn{
		 padding: 10rpx 0;
		 text-align: center;
	 }
 }
 .bold{
	 font-weight: 600;
	 padding: 20rpx 0;
 }
 .cu-list{
	  border-radius: 20px;
		padding: 10rpx 0;
	 .cu-item{
		 padding: 20rpx;
		 .cu-avatar{
			 width: 80rpx;
			 height: 80rpx;
			 margin-right: 26rpx;
		 }
		 .date{
			 color: #666;
			 font-size: 24rpx;
		 }
	 }
	 .cu-btn{
		width: 100%;
		background-color: #fff; 
		justify-content: space-between;
		
	 }
 }
</style>
