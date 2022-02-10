<template>
	<view class="status_bar">
		<view class="content">
			<view class="q-title-search">
			  <text class="text">期货原油宝</text>
			  <view class="search">
			    <u-search 
			      placeholder="搜索期货hot话术" 
				  bg-color="" 
			      border-color="#FDF6EC"
				  placeholderColor="#FFFFFF"
				  color="#FFFFFF"
				  searchIconColor="#FFFFFF"
			      shape="round" 
				  :show-action="false" 
			      v-model="keyword"
			      @change="onSearch">
			    </u-search>
			  </view>
			</view>
			<!-- banner -->
			<view class="noticeView"></view>
			<view class="u-demo-block">
				<u-swiper
						:list="list3"
						previousMargin="50"
						nextMargin="50"
						circular
						:autoplay="false"
						radius="0"
						bgColor="#FDF6EC"
						indicator
						indicatorMode="line"
				></u-swiper>
			</view>
			<view class="noticeView_bot">
			      <u-notice-bar bgColor="" icon="" :text="text1"></u-notice-bar>
			</view>
			
			<!-- 话术 -->
			<view class="huashuview">
				<view class="qhgridView_top">
					<image class="shugang" src="/static/paihangbang.png" mode=""></image>
					<text style="margin-left: 10px;color: #000000;">期货搜索榜</text>
				</view>
				<view class="taglist">
					<view style="margin: 5px 10px;" v-for="item in indexList" :key="item.name">
						<u-tag @click="tagclick(item)" shape="circle" :text="item.name" plain plainFill borderColor="#efefef" color="#666" bgColor="#F6F6F6"> </u-tag>
					</view>
				</view>
			</view>
			<view class="scrolllist">
				<u-scroll-list @right="right" @left="left">
					<view class="scroll-list" style="flex-direction: row;">
						<view
								class="scroll-list__goods-item"
								v-for="(item, index) in list4"
								:key="index"
								:class="[(index === 1) && 'scroll-list__goods-item--no-margin-right']"
						>
							<image class="scroll-list__goods-item__image" :src="item.thumb"></image>
							<text class="scroll-list__goods-item__text">￥{{ item.price }}</text>
						</view>
						<view class="scroll-list__show-more">
							<text class="scroll-list__show-more__text">查看更多</text>
							<u-icon name="arrow-leftward" color="#666666" size="12"></u-icon>
						</view>
					</view>
				</u-scroll-list>
			</view>
		</view>
		
		<!-- <view class="content"> -->
			<!-- Logo-牛 -->
			<!-- <view class="bigview"> -->
				<!-- <view class="Card_0"></view> -->
			<!-- </view> -->
			<!-- 通知 -->
			<!-- <view class="noticeView">
			      <u-notice-bar :text="text1"></u-notice-bar>
			</view> -->
			<!-- <view class="qhgridView_top">
				<image class="shugang" src="/static/paihangbang.png" mode=""></image>
				<text style="margin-left: 10px;color: #ffffff;">今日期货霸榜</text>
			</view> -->
		<!-- </view> -->
		<!-- <u-gap height="40" bg-color="#fff"></u-gap> -->
		<!-- <u-list style="height: auto;">
			<u-list-item
				v-for="(item, index) in newsListData"
				:key="index"
				 
			>
				<u-cell :title="`${item.title}`" @click="jumpHotnewsdetail(item)">
					<u-avatar
						slot="icon"
						shape="square"
						size="35"
						:src="item.thumb"
						customStyle="margin: -3px 5px -3px 0"
					></u-avatar>
				</u-cell>
			</u-list-item>
		</u-list> -->
		<!-- <u-gap height="40" bg-color="#fff"></u-gap> -->
		<!-- <u-gap height="40" bg-color="#fff"></u-gap> -->
	</view>
</template>

<script>
	import {TOPTHDATA, ListHQ, newsList} from './homePageDataTop.js'
export default {
	data() {
		return {
			indicator: true,
			list4: [{
				price: '230.5',
                thumb: 'https://cdn.uviewui.com/uview/goods/1.jpg'
			}, {
				price: '74.1',
                thumb: 'https://cdn.uviewui.com/uview/goods/2.jpg'
			}, {
				price: '8457',
                thumb: 'https://cdn.uviewui.com/uview/goods/6.jpg'
			}, {
				price: '1442',
                thumb: 'https://cdn.uviewui.com/uview/goods/5.jpg'
			}, {
				price: '541',
                thumb: 'https://cdn.uviewui.com/uview/goods/2.jpg'
			}, {
				price: '234',
                thumb: 'https://cdn.uviewui.com/uview/goods/3.jpg'
			}, {
				price: '562',
                thumb: 'https://cdn.uviewui.com/uview/goods/4.jpg'
			}, {
				price: '251.5',
                thumb: 'https://cdn.uviewui.com/uview/goods/1.jpg'
			}],
			list3: [
				'https://cdn.uviewui.com/uview/swiper/swiper3.png',
				'https://cdn.uviewui.com/uview/swiper/swiper2.png',
				'https://cdn.uviewui.com/uview/swiper/swiper1.png',
			],
			filterList: false,
			keyword: '',
			loginState: uni.getStorageSync('login_key'),
			newlist:  ['国际资讯', '国内资讯', '更多资讯'],
			curNow: 0,
			newsListdatas: newsList,
			newsListData: newsList.slice(0, 5),
			indexList: ListHQ.slice(3, 11),
			topthrdata: TOPTHDATA,
			text1: '修订棉花期货合约规则，助力提升服务实体经济能力'
		}
	},
	onLoad() {
		 
	},
	created() {
		this.newsListData = this.newsListdatas.slice(0, 5)
	},
	methods: {
		left() {
			console.log('left');
		},
		right() {
			console.log('right');
		},
		onSearch () {
		  if (this.$u.trim(this.keyword)) {
		    this.filterList = this.topSymbols.filter((item) => {
		      return item.title.toLocaleUpperCase().indexOf(this.$u.trim(this.keyword.toLocaleUpperCase())) != -1
		    })
		  } else {
		    this.filterList = false
		  }
		},
		tagclick(symbol) {
		  uni.navigateTo({
			url: '/pages/SecView/lineDetail?item='+ encodeURIComponent(JSON.stringify(symbol))
		  })
		},
		jumpHotnewsdetail(item) {
			uni.navigateTo({
				url: '/pages/ThrView/hotnewsdetail?item='+ encodeURIComponent(JSON.stringify(item))
			});
		},
		zixuan(item,index) {
		     
			this.tianjiazixuan(item,index)
		},
		tianjiazixuan(items,index) {
			let that = this
			if (this.loginState == 1) {
				var list = uni.getStorageSync('ListHQZHIXUANDATA_key')?JSON.parse(uni.getStorageSync('ListHQZHIXUANDATA_key')): []
				 
					list.push(items)
					uni.showToast({
					  icon: 'none',
					  title: '加入自选成功'
					});
				 
				uni.setStorageSync('ListHQZHIXUANDATA_key', JSON.stringify(list)) 
			} else {
				uni.showToast({
				  icon: 'none',
				  title: '当前未登录，请先登录后再进行操作'
				});
			}
		},
		sectionChange(index) {
			this.newsListData = []
			this.curNow = index;
			if (index == 0) {
				this.newsListData = this.newsListdatas.slice(0, 5)
			} else if (index == 1 ) {
				this.newsListData = this.newsListdatas.slice(5, 10)
			} else {
				this.curNow = 0
				this.newsListData = this.newsListdatas.slice(0, 5)
				
				// uni.switchTab({
				// 	url: '/pages/ThrView/fhrview'
				// })
				uni.navigateTo({
					url:'../ThrView/fhrview'
				})
			}
		},
		btn() {
			uni.navigateTo({
				url: '../SecView/secview'
			})
		}
	},
}
</script>


<style lang="scss" scoped>
	.q-title-search {
	  display: flex;
	  align-items: center;
	  justify-content: space-between;
	  padding: 16rpx 60rpx;
	  .text {
	    font-size: 40rpx;
	    color: #FFFFFF;
	  }
	}
	.content {
		text-align: center;
		padding-bottom: 0;
		padding-bottom: constant(safe-area-inset-bottom);  
		padding-bottom: env(safe-area-inset-bottom);  
		overflow: hidden;
		background: url(@/static/homered.png)  fixed center center;
		min-height: 100vh;
		// background-size:100% 270px; 
		.bigview {
			margin-top: 0rpx;
			.Card_0 {
				background: url(@/static/titleLogo_ny.bcb4964.png) no-repeat fixed top center;
				background-size: 100% 150px;
				background-position: top left;
				display: block;
				height: 150px;
				z-index: 1;
			} 
		}
		.noticeView {
			// padding: 10px;
			height: 35px;
			margin: 10px 0 0 0;
			width: 100%;
			border-radius: 100px 100px 0 0;
			background-color: rgba(253,246,236,1);
		}
		
		.noticeView_bot {
			// margin: 10px 0 0 0;
			width: 100%;
			border-radius: 0 0 100px 100px ;
			background-color: rgba(253,246,236,1);
		}
		.huashuview {
			margin: 10px 15px;
			min-height: 200px;
			border-radius: 10px ;
			background-color: rgba(253,246,236,1);
			.qhgridView_top {
				padding: 50rpx 0 20px 20px;
				display: flex;
				align-items: center;
				.shugang {
					width: 20px;
					height: 20px;
				}
			}
			.taglist {
				margin: 0px 10px;
				display: flex;
				overflow: hidden;
				flex-wrap: wrap;
			}
		}
		.scrolllist {
			margin: 0 15px;
			.scroll-list {
				@include flex(column);
			
				&__goods-item {
					margin-right: 20px;
					background-color: #fff;
					&__image {
						width: 60px;
						height: 60px;
						border-radius: 4px;
					}
			
					&__text {
						color: #333;
						text-align: center;
						font-size: 12px;
						margin-top: 5px;
					}
				}
			
				&__show-more {
					background-color: #fff0f0;
					border-radius: 3px;
					padding: 3px 6px;
					@include flex(column);
					align-items: center;
			
					&__text {
						font-size: 12px;
						width: 12px;
						color: #666666;
						line-height: 16px;
					}
				}
			}
		}
		
		
		
		
		
		
		
		
		
		
		
		.paihangbangview {
			background-color: #efefef;
			margin: 0 20px 0px 20px; 
			border-top-right-radius: 50px;
			border-top-left-radius: 50px;
		}
		.top_thr {
			display: flex;
			justify-content: center;
			margin-top: 50px;
			.no_top {
				margin-top: -25px;
			}
			.qihuo_2 {
				margin-top: 20px;
				display: flex;
				flex-direction: column;
			}
			.top_2 {
				background-color: #FFFFFF;
				width: 90px;
				height: 90px;
				border-radius: 45px;
				margin-right: 30px;
				margin-top: -15px;
				color: green;
				box-shadow: 0px -1px 0px 0px #e5e5e5,   /*上边阴影 */
							-0.2px 0px 0px 0px #e5e5e5,   /*左边阴影  */
							0.2px 0px 0px 0px #e5e5e5,    /*右边阴影 */
							0px 1px 0px 0px #e5e5e5;     /*下边阴影 */
			}
			.top_1 {
				background-color: #FFFFFF;
				width: 90px;
				height: 90px;
				border-radius: 45px;
				margin-top: -50px;
				color: red;
				box-shadow: 0px -1px 0px 0px #e5e5e5,   /*上边阴影 */
							-0.2px 0px 0px 0px #e5e5e5,   /*左边阴影  */
							0.2px 0px 0px 0px #e5e5e5,    /*右边阴影 */
							0px 1px 0px 0px #e5e5e5;     /*下边阴影 */
			}
			.top_3 {
				background-color: #FFFFFF;
				width: 90px;
				height: 90px;
				border-radius: 45px;
				margin-left: 30px;
				margin-bottom: 20px;
				color: gray;
				box-shadow: 0px -1px 0px 0px #e5e5e5,   /*上边阴影 */
							-0.2px 0px 0px 0px #e5e5e5,   /*左边阴影  */
							0.2px 0px 0px 0px #e5e5e5,    /*右边阴影 */
							0px 1px 0px 0px #e5e5e5;     /*下边阴影 */
			}
		}
		
	}
	.status_bar {
	  height: var(--status-bar-height);
	  width: 100%;
	}
</style>
