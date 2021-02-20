<template>
	<view class="container">
		<cu-custom bgColor="nav-bg" :isBack="true" :isShow="true">
			<block slot="backText">爱车档案</block>
		</cu-custom>
		<view class="content">
			<view class="head bg-white  add-box" v-if="state == '1'">
				<view style="margin-bottom: 40rpx;">
					您暂未添加爱车，赶紧添加定制
				</view>
				<button class="cu-btn bg-themeColor round lg" @tap="add">添加爱车</button>
			</view>
			<view  class="mar-30" v-if="state == '0'">
				<view class="head bg-white  list-box flex-z mar-30"  v-for="(item, index) in list" :key="index">
					<view class="flex-c">
						<image src="../../../static/icon/4.png" mode=""></image>
						<view>
							<view class="flex-c">
						    <view class="text-black">{{ item.title }} </view>
								<view class="tag" v-if="item.status == 1">默认</view>
							</view>
							<view class="pad-10" style="font-size: 12px; color: #666;">
								{{ item.type }}
							</view>
						</view>
					</view>
					<button class="cu-btn update-btn" @tap="add('update')">编辑</button>
				</view>
			</view>
			
		</view>
		<view class="flex-direction btn">
			<button v-if="state == '0'" class="cu-btn bg-themeColor lg" @tap="add('add')">添加</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				state: '0',
				list:[
					{
						title: '川AS1252',
						type: '一汽大众奥迪-A4L',
						status: '1'
					},
					{
						title: '川AS1252',
						type: '一汽大众奥迪-A4L',
						status: '0'
					},
					{
						title: '川AS1252',
						type: '一汽大众奥迪-A4L',
						status: '0'
					}
				]
			};
		},
		methods:{
			// 添加
			add(val){
				if(val == 'add'){
					 uni.navigateTo({
					 	url: '/pages/pagesB/addCard/addCard?title=爱车档案&type=1'
					 })
				}else{
					uni.navigateTo({
						url: '/pages/pagesB/addCard/addCard?title=编辑车辆&type=2'
					})
				}
			
			}
		}
	}
</script>

<style lang="scss" scoped>
	.add-box{
		padding: 60rpx;
		text-align: center;
		font-size: 14px;
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
	.list-box{
		image{
			width: 120rpx;
			height: 120rpx;
			margin-right: 20rpx;
		}
		.text-black{
			font-weight: 600;
		}
		.tag{
      padding: 0rpx 10rpx;
			background: #29BF54;
			border-radius: 10rpx;
			color: #fff;
			font-size: 20rpx;
			margin-left: 20rpx;
		}
	.update-btn{
		 margin: 0;
		 padding: 0;
		 border: none!important;
		 background-color: transparent;
		 font-size: 14px;
		 color: #999;
	}

	}
</style>
