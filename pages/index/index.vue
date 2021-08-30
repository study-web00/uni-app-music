<template>
	<view class="content">
		<view class="page-section-spacing">
			<swiper class="swiper" :autoplay="true" interval="1000" indicator-dots indicator-active-color="#DD524D">
				<swiper-item v-for="(item,index) in swiperList" :key="index">
					<image :src="item.imageUrl" class="swiper-image" mode="widthFix"></image>
				</swiper-item>
			</swiper>
		</view>
		<view class="title">
			<text>推荐歌单</text>
		</view>
		<scroll-view :scroll-y="true" class="recommend_content">

			<view class="recommend_item" v-for="(item,index) in personalized" :key="index">
				<view class="recommend_image">
					<image :src="item.picUrl" mode="aspectFill"></image>
				</view>
				<view class="recommend_name">{{item.name}}</view>
			</view>

		</scroll-view>

	</view>

</template>

<script>
	export default {
		data() {
			return {
				// 轮播图数据
				swiperList: [],
				// 推荐歌单
				personalized: []
			}
		},
		onLoad() {
			const serverUrl = this.serverUrl
			uni.request({
					url: serverUrl + '/banner',
					method: "GET",
					success: (res) => {
						if (res.data.code === 200) {
							this.swiperList = res.data.banners
							console.log(this.swiperList)
						}
					}
				}),
				uni.request({
					url: serverUrl + '/personalized',
					method: "GET",
					success: (res) => {
						if (res.data.code === 200) {
							this.personalized = res.data.result
							console.log(res.data.result)
						}
					}
				})
		},
		methods: {

		}
	}
</script>

<style>
	@import url("index.css");
</style>
