<template>
	<view class="goods-list">
		<view class="goods-item" @click="navigator(item.id)" v-for="item in goods" :key="item.id">
			<image :src="item.img_src"></image>
			<view class="price">
				<text>{{item.price_new}}</text>
				<text>{{item.price_old}}</text>
			</view>
			<view class="name">{{item.name}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			navigator(id){
				this.$emit('goodsItemClick',id)
			}
		},
		props:['goods']
	}
</script>

<style lang="scss">
.goods-list{
			padding: 0 15rpx;
			display: flex;
			flex-wrap: wrap;
			justify-content: space-between;
			.goods-item{
				background: #FFFFFF;
				width: 355rpx;
				margin: 10rpx 0;
				padding: 15rpx;
				box-sizing: border-box;
				image{
					width: 80%;
					height: 150px;
					display: block;
					margin: auto;
				}
				
				.price{
					color: $shop-color;
					font-size: 36rpx;
					margin:20rpx 0 5rpx 0;
					text:nth-child(2){
						color: #CCCCCC;
						font-size: 28rpx;
						margin-left: 17rpx;
						text-decoration: line-through;
					}
				}
				
				.name{
					font-size: 28rpx;
					line-height: 50rpx;
					padding-bottom: 15rpx;
					padding-top: 10rpx;
				}
				
			}
			
		}
</style>
