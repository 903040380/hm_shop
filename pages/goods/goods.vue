<template>
	<view>
		<goods-list @goodsItemClick="goGoodsDetail" :goods="goods"></goods-list>
		<view class="isOver" v-if="flag">
			-----我是有底线的-----
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				pageIndex:1,
				goods:[],
				flag:false,
				total:0
			}
		},
		methods: {
			async getGoodsList(callBack){
				console.log('获取商品数据')
				const res = await this.$myRequest({
					url:'/get/goods?pageIndex='+this.pageIndex
				})
				console.log(res)
				this.goods = [...this.goods,...res.data.goods]
				this.total=res.data.total
				callBack && callBack()
			},
			goGoodsDetail(id){
				uni.navigateTo({
					url:'/pages/goods-detail/goods-detail?id='+id
				})
			}
			
		},
		onLoad(){
			this.getGoodsList()
		},
		onReachBottom(){
			console.log('触底')
			if(this.goods.length>=this.total){
				return this.flag = true
			}
			
			this.pageIndex++
			this.getGoodsList()
		},
		onPullDownRefresh() {
			console.log('刷新')
			this.pageIndex=1
			this.goods=[]
			this.flag=false
			setTimeout(()=>{
				this.getGoodsList(()=>{
					uni.stopPullDownRefresh()
				})
			},300)
			
		},
		components:{
			"goods-list":goodsList
		}
	}
</script>

<style lang="scss">
	page{
		background-color: #EEEEEE;
	}
	.isOver{
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		background-color: #FFFFFF;
	}
</style>
