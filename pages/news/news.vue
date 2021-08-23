<template>
	<view class="news">
		<news-item :list=newsList @itemClick="goDetail"></news-item>
	</view>
</template>

<script>
	import newsList from '../../components/news-item/news-item.vue'
	export default {
		data() {
			return {
				newsList:[]
			}
		},
		methods: {
			async getNews(){
				const res = await this.$myRequest({
					url:'/get/newslist'
				})
				console.log(res)
				this.newsList = res.data.newslist
			},
			goDetail(id){
				uni.navigateTo({
					url:'/pages/news-detail/news-detail?id='+id
				})
			}
		},
		onLoad() {
			this.getNews()
		},
		components:{"news-item":newsList}
	}
</script>

<style lang="scss">
	
</style>
