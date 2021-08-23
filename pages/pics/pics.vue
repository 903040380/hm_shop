<template>
		<view class="pics">
			<scroll-view class="left" scroll-y="true">
				<view @click="leftClickHandle(index,item.id)" :class="active===index?'active':''" v-for="(item,index) in cates" :key="item.id">
					{{item.title}}
				</view>
			</scroll-view>
		</view>
</template>

<script>
	export default {
		data() {
			return {
				cates:[],
				active:0
			}
		},
		methods: {
			async getPicsCate(){
				const res = await this.$myRequest({
					url:'/get/picscate'
				})
				console.log(res)
				this.cates = res.data.picscate
			},
			async leftClickHandle(index,cateId){
				this.active=index
				const res = await this.$myRequest({
					url:'/get/cateimage/'+cateId
				})
				console.log(res)
			}
		},
		onLoad() {
			this.getPicsCate()
		}
	}
</script>

<style lang="scss">
page{
	height: 100%;
}
.pics{
	height: 100%;
	.left{
		width: 200rpx;
		height: 100%;
		border-right: 1px solid #EEEEEE;
		view{
			height: 60px;
			line-height: 60px;
			color: #333333;
			text-align: center;
			font-size: 30rpx;
			border-bottom: 1px solid #EEEEEE;
		}
		.active{
			background-color: $shop-color;
			color: #FFFFFF;
		}
	}
}
</style>
