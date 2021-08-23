<template>
	<view class="contact">
		<image src="https://i1.mifile.cn/f/i/2018/service/serviceCenter_img2.jpg"></image>
		<view class="info">
			<view @click="call">联系电话：777-777-7777 (点击拨打)</view>
			<view>公司地址：江苏省苏州市工业园区河马科技园7号楼707</view>
		</view>
		<map class="map" :scale="scale" :markers="markers" :longitude="longitude" :latitude="latitude"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:120.532819,
				latitude:31.284809,
				scale:13,
				markers:[
					{
					longitude:120.532819,
					latitude:31.284809,
					iconPath:'../../static/logo.png',
					width:30,
					height:30
					}
				]
			}
		},
		methods: {
			call(){
				uni.makePhoneCall({
					phoneNumber:'777-777-7777'
				})
			}
		}
	}
</script>

<style lang="scss">
.contact{
	image{
		width: 750rpx;
		height: 320rpx;
	}
	.info{
		padding: 10rpx 20rpx;
		font-size: 30rpx;
		view{
			line-height: 60rpx;
			border-bottom: 1px solid #EEEEEE;
		}
	}
	.map{
		width: 750rpx;
		height: 750rpx;
	}
}
</style>
