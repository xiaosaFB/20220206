<!-- 资讯>搜索 -->
<template>
	<view class="search">
		<u-row justify="space-between">
			<u-col span="12">
				<u--input class="search-left" placeholder="恒大 | 28亿存款质押" prefixIcon="search" shape="circle" focus
					prefixIconStyle="color: #909399"></u--input>
			</u-col>
		</u-row>
		<u-divider text="热门搜索" textColor="#ff0000" lineColor="#ff0000"></u-divider>
		<!-- <u-row justify="start">
			<u-tag style="margin: 0 10px;" type="warning" v-for="(item,index) in hotData" :key='index' :text="index+1+'、'+item" size="mini" ></u-tag>
		</u-row> -->
		<u-grid :border="false" @click="click" :col="2">
			<u-grid-item v-for="(item,index) in hotData" :key='index' style="margin: 2px 0;align-items: start;">
				<u-tag style="margin: 0 10px;" type="warning" :text="index+1+'、'+item" size="mini"></u-tag>
			</u-grid-item>
		</u-grid>
		<u-divider text="历史搜索" textColor="#2979ff" lineColor="#2979ff"></u-divider>
		<u-row justify="start">
			<!-- :show="close1" @close="close1 = false" -->
			<u-tag v-for="(item,index) in hstoryData" :key='index' :text="item" size="mini" closable icon="tags-fill">
			</u-tag>
		</u-row>
		<u-alert style="margin-top: 20px;" type="warning" :show-icon="true" :closable="true" :description = "description"></u-alert>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				hotData: ["恒大", "28亿存款质押", "元宇宙", "马斯克", "国内疫情", "储存物资", "房地产税", "比特币", "中美关系", "新冠疫苗"],
				hstoryData: ["我的父辈们", "冬奥会"],
				description:"通知被关闭，无法收到突发新闻消息",
			}
		},
		onLoad() {},
		methods: {
			click(name) {
				this.$refs.uToast.success(`点击了第${name}个`)
			}
		}
	}
</script>

<style lang="scss" scoped>
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
</style>
