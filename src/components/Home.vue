<template>
	<div>
		<tab :line-width="1" custom-bar-width="60px">
			<tab-item @on-item-click="changeNav" selected>首页</tab-item>
			<tab-item @on-item-click="changeNav" >新歌</tab-item>
			<tab-item @on-item-click="changeNav" >排行</tab-item>
		</tab>
		<swiper  dots-position="center">
			<swiper-item class="swiper-nav" v-for="(item, index) in bannerList" :key="index">
				<img :src="item" />
			</swiper-item>
		</swiper>
	</div>
</template>

<script>
	import {Tab, TabItem, Swiper, SwiperItem} from 'vux';
	import http from "../http/index.js";

	export default {
		name: 'Home',
		data () {
			return {
				bannerList: ['static/img/banner1.jpg', 'static/img/banner2.jpg', 'static/img/banner3.jpg']
			}
		},
		components: {
			Tab,
			TabItem,
			Swiper,
			SwiperItem
		},
		methods: {
			changeNav() {

			}
		},
		created() {
			// this.$vux.loading.show();
			http.get('/213-4',{
					params: {
							topid: 4
					}
			})
			.then((res) => {
					console.log(res);
			})
			.catch((err) => {
					console.log(err);
			});
		}
	}
</script>

<style lang="less" scoped>
.swiper-nav img {
	width: 100%;
}
 
</style>
