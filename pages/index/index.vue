<template>
	<view class="home">
		<swiper indicator-dots="true" circular="true">
			<swiper-item v-for="item in swipers" :key="item.id">
				<image :src="item.img_src"></image>
			</swiper-item>
		</swiper>
		
		<view class="nav">
			<view class="nav-item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		
		<view class="hot-goods">
			<view class="title">
				推荐商品
			</view>
			<goods-list @goodsItemClick="goGoodsDetail" :goods="goods"></goods-list>
		</view>
		
	</view>
	
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				swipers:[],
				goods:[],
				navs:[
					{
						icon:'cuIcon-shop',
						title:'河马超市',
						path:'/pages/goods/goods'
					},
					{
						icon:'cuIcon-new',
						title:'联系我们',
						path:'/pages/contact/contact'
					},
					{
						icon:'cuIcon-pic',
						title:'社区图片',
						path:'/pages/pics/pics'
					},
					{
						icon:'cuIcon-video',
						title:'学习视频',
						path:'/pages/videos/videos'
					}
				]
			}
		},
		methods: {
			async getSwipers(){
				console.log('获取轮播图数据');
				// uni.request({
				// 	url:'http://localhost:3000/api/get/banner',
				// 	success:(res)=>{
				// 		console.log('测试')
				// 		console.log(res)
				// 	}
				// })
				
				const res = await this.$myRequest({
					url:'/get/banner'
				})
				console.log(res)
				this.swipers = res.data.banner
				console.log(this.swipers)
			},
			
			async getHotGoods(){
				console.log('获取热门商品数据');
				const res = await this.$myRequest({
					url:'/get/hotgoods'
				})
				console.log(res)
				this.goods = res.data.hotgoods
				console.log(this.goods)
			},
			
			navItemClick (url){
				uni.navigateTo({
					url:url
				})
			},
			goGoodsDetail(id){
				uni.navigateTo({
					url:'/pages/goods-detail/goods-detail?id='+id
				})
			}
		},
		onLoad(){
			this.getSwipers()
			this.getHotGoods()
		},
		components:{
			"goods-list":goodsList,
		}
	}
</script>

<style lang="scss">
	.home{
		swiper{
			width: 750rpx;
			height: 380rpx;
			image{
				height: 100%;
				width: 100%;
			}
		}
	}
	
	.nav{
		display: flex;
		.nav-item{
			width: 25%;
			text-align: center;

			view{
				width: 120rpx;
				height: 120rpx;
				background: $shop-color;
				border-radius: 60rpx;
				margin: 10rpx auto;
				line-height: 120rpx;
				color: #FFFFFF;
				font-size: 50rpx;
			}
			
			text{
				font-size: 30rpx;
			}
			
		}
	}

	.hot-goods{
		background-color: #EEEEEE;
		margin-top: 20rpx;
		overflow: hidden;
		.title{
			height: 100rpx;
			line-height: 100rpx;
			color: $shop-color;
			text-align: center;
			letter-spacing: 20px;
			background-color: #FFFFFF;
			margin: 7rpx 0;
			font-size: 35rpx;
		}
		
		
	}
	
</style>
