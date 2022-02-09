<template>
	<view class="status_bar">
		
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
			loginState: uni.getStorageSync('login_key'),
			newlist:  ['国际资讯', '国内资讯', '更多资讯'],
			curNow: 0,
			newsListdatas: newsList,
			newsListData: newsList.slice(0, 5),
			indexList: ListHQ.slice(0, 7),
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
		toKline (symbol) {
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
	.content {
		text-align: center;
		padding-bottom: 0;
		padding-bottom: constant(safe-area-inset-bottom);  
		padding-bottom: env(safe-area-inset-bottom);  
		overflow: hidden;
		background: url(@/static/homebg.png) no-repeat fixed top center;
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
			padding: 10px;
			margin: 10px 0 0 15%;
			width: 70%;
			border-radius: 100px;
			background-color: rgba(253,246,236,1);
		}
		.qhgridView_top {
			padding: 50rpx 0 20px 20px;
			display: flex;
			align-items: center;
			.shugang {
				width: 40px;
				height: 40px;
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
