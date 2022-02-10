<!-- 资讯 -->
<template>
	<view class="zx">
		<view class="search">
			<u-row justify="space-between">
				<u-col span="10">
					<u--input class="search-left" placeholder="恒大 | 28亿存款质押" prefixIcon="search" shape="circle"
						@focus="focusInput" prefixIconStyle="color: #909399"></u--input>
				</u-col>
				<u-col span="2">
					<u-button class="btn-msg" icon="email" :plain="true" text="" @click="msgClick"></u-button>
					<!-- <u-badge type="error" max="99" value="18"></u-badge> -->
				</u-col>
			</u-row>
		</view>
		<u-sticky bgColor="#fff">
			<u-tabs :current="tabIndex" :activeStyle="{
						color: '#303133',
						fontWeight: 'bold',
						transform: 'scale(1.05)'
					}" :inactiveStyle="{
						color: '#606266',
						transform: 'scale(1)'
					}" @click="tabClick" :list="list1"></u-tabs>
		</u-sticky>
		<view class="page-one">
			<u-list @scrolltolower="scrolltolower">
				<u-list-item v-for="(item, index) in indexList" :key="index">
					<u-cell :title="`列表长度-${index + 1}`">
						<u-avatar slot="icon" shape="square" size="35" :src="item.url"
							customStyle="margin: -3px 5px -3px 0"></u-avatar>
					</u-cell>
				</u-list-item>
			</u-list>
		</view>
	</view>
</template>

<script>
	import {
		newsList
	} from '../FirstView/homePageDataTop.js';
	export default {
		data() {
			return {
				newsListData: newsList,
				list1: [{
					name: '要闻',
					badge: {
						isDot: true
					}
				}, {
					name: '热点',
					badge: {
						value: 5,
					}
				}, {
					name: '期货'
				}],
				tabIndex: 0,
				indexList: [],
				urls: [
					'https://cdn.uviewui.com/uview/album/1.jpg',
					'https://cdn.uviewui.com/uview/album/2.jpg',
					'https://cdn.uviewui.com/uview/album/3.jpg',
					'https://cdn.uviewui.com/uview/album/4.jpg',
					'https://cdn.uviewui.com/uview/album/5.jpg',
					'https://cdn.uviewui.com/uview/album/6.jpg',
					'https://cdn.uviewui.com/uview/album/7.jpg',
					'https://cdn.uviewui.com/uview/album/8.jpg',
					'https://cdn.uviewui.com/uview/album/9.jpg',
					'https://cdn.uviewui.com/uview/album/10.jpg',
				]
			}
		},
		onLoad() {
			this.loadmore()
		},
		methods: {
			focusInput() {
				uni.navigateTo({
					url: '/pages/ThrView/hotnewsdetail?item='
				});
			},
			msgClick() {
				uni.navigateTo({
					url: '/pages/ThrView/hotnewsdetail?item='
				});
			},
			tabClick(item) {
				this.tabIndex = item.index
			this.loadmore()
			},
			scrolltolower() {
				this.loadmore()
			},
			loadmore() {
				for (let i = 0; i < 30; i++) {
					this.indexList.push({
						url: this.urls[uni.$u.random(0, this.urls.length - 1)]
					})
				}
			},
			jumpHotnewsdetail(item) {
				uni.navigateTo({
					url: '/pages/ThrView/hotnewsdetail?item=' + encodeURIComponent(JSON.stringify(item))
				});
			},
			//首页头部tab点击切换
			IsHeadTabClick: function(index, item) {
				this.headTabIdx = index;
			},

		}
	}
</script>

<style lang="scss" scoped>
	.zx {
		min-height: 100vh;

		.search {
			padding: 5px;

			.search-left {
				padding: 5px !important;
			}

			.uni-input-placeholder {
				font-size: 13px;
				letter-spacing: 1px;
			}
		}
		.page-one{
			height: 100vh;
		}
		.btn-msg {
			background-color: transparent;
			border: none;

		}

	}
</style>
