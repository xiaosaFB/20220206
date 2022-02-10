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
						imgMode="scaleToFill"
						indicatorMode="line"
						@click="swiperclick"
				></u-swiper>
			</view>
			<view class="noticeView_bot">
			      <u-notice-bar bgColor="" icon="" :text="text1"></u-notice-bar>
			</view>
			
			<!-- 话术 -->
			<view class="huashuview">
				<view class="qhgridView_top">
					<image class="shugang" src="/static/paihangbang.png" mode=""></image>
					<text style="margin-left: 10px;color: #000000;">【期货热门搜索榜】</text>
				</view>
				<view class="taglist">
					<view style="margin: 5px 10px;" v-for="item in indexList" :key="item.name">
						<u-tag @click="tagclick(item)" shape="circle" :text="item.name" plain plainFill borderColor="#efefef" color="#666" bgColor="#F6F6F6"> </u-tag>
					</view>
				</view>
			</view>
			<view class="huashuview">
				<view class="qhgridView_top">
					<image class="shugang" src="/static/paihangbang.png" mode=""></image>
					<text style="margin-left: 10px;color: #000000;">【期货冷门黑马榜】</text>
				</view>
				<view class="scrolllist">
					<u-scroll-list @right="right" @left="left">
						<view class="scroll-list" style="flex-direction: row;">
							<view
									class="scroll-list__goods-item"
									v-for="(item, index) in topthrdata"
									:key="index"
									:class="[(index === 1) && 'scroll-list__goods-item--no-margin-right']"
									@click="lengmen(item)"
							>
								<image class="scroll-list__goods-item__image" src="../../static/headhuangguan.png"></image>
								<view style="margin-top: 17px;background-color: #D62D34;width: 75px; height: 75px;border-radius: 50%;display: flex;flex-direction: column;justify-content: center;align-items: center;">
									<text class="scroll-list__goods-item__text" style="color: #FFF;">{{ item.name }}</text>
									<text class="scroll-list__goods-item__text" style="color: #FFF;">{{ item.jiage }}</text>
									<text class="scroll-list__goods-item__text" style="color: #FFF;">+{{ item.zhangfu }}%</text>
								</view>
								
							</view>
							<view class="scroll-list__show-more" @click="lengmenmore">
								<text class="scroll-list__show-more__text">查看更多</text>
								<u-icon name="arrow-leftward" color="#666666" size="12"></u-icon>
							</view>
						</view>
					</u-scroll-list>
				</view>
			</view>
			<view class="huashuview">
				 <swiper class="swiper" indicator-active-color='#fff' :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
				 	<swiper-item v-for="(item,index) in bannerList" :key='index' @click="JumpFuneralNews(index,item)">
				 		<view class="swiper-item uni-bg-red">
				 			<image :src="item.imgs"></image>
				 		</view>
				 		<view class="swiper-title">
				 			<view class="swiper-title-box">{{ item.title }}</view>
				 		</view>
				 	</swiper-item>
				 </swiper>
				 <view class="contBg">
				 	<view class="contOver" v-for="(item,index) in contOneList" :key="index" @click="jumpHotnewsdetail(item)">
				 		<view class="idxMainBox">
							<view class="contRtImg"><image :src="item.imgs"></image></view>
				 			<view class="contOverLt">
				 				<view class="contTxt">{{ item.title }}</view>
				 				<view class="contTime">{{ item.author }} {{ item.updateTime }}</view>
				 			</view>
				 		</view>
				 	</view>
				 </view>
				 <view class="shopOver">
				 	<view class="contTitle">
				 		<view class="idxMainBox">推荐热门</view>
				 	</view>
				 	<view class="idxMainBox">
				 		<view class="shopLt" v-for="(item,index) in contTwoList" :key='index' @click="jumpHotnewsdetail(item)">
				 			<view class="shopImg"><image :src="item.imgs" mode="aspectFill"></image></view>
				 			<view class="shopTxt">{{ item.name }}</view>
				 			</view>
				 	</view>
				 </view>
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
			list3: [
				'../../static/pic_16313389660307i86GGRlVL5O-EEEgCeXs.png',
				'../../static/pic_1631338.png',
				'https://img1.baidu.com/it/u=2643548377,3443601659&fm=253&fmt=auto&app=138&f=JPEG?w=550&h=342.png',
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
			text1: '粳米期货一周岁：产业多策略积极参与套保粳米期货一周岁：产业多策略积极参与套保',
			bannerList:[
				{ id:1, imgs:'https://img2.baidu.com/it/u=1484456337,1126487471&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=309' },
				{ id:2, imgs:'https://img0.baidu.com/it/u=3284388619,708735942&fm=253&fmt=auto&app=120&f=JPEG?w=550&h=342' }
			],//轮播图
			/*图片轮播*/
			indicatorDots: true,
			autoplay: true,
			interval: 2000,
			duration: 500,
			contOneList:[
				{ id:1, title:'粳米期货一周岁：产业多策略积极参与套保', author:'平台', updateTime:'2022-01-30', imgs:'https://img1.baidu.com/it/u=65051305,761009287&fm=253&fmt=auto&app=120&f=PNG?w=735&h=500',html: `<div class="details">
											
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">随着居民生活水平不断提高，市场对优质稻米的需求也随之增加，越来越多的优质稻品种涌向市场，“普改优”已成为稻米产业种植结构调整的重要方向。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">优质晚籼稻是加工小包装商品米所需的主要原料，其价格波动会给企业造成较大的生产经营风险。为更好满足企业的加工和套期保值需求，为企业提供有效的风险管理工具，2020年7月份，郑商所对晚籼稻期货交割标准进行了修订。</span> 
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">日前，郑商所相关负责人介绍，此次交割标准修订主要内容为：一是优化交割指标体系，将期货交割标的物定位于优质晚籼稻；二是调整替代交割品贴水幅度，充分体现“优质优价”原则；三是收严入库储存品质判定指标，避免储存品质较差的晚籼稻参与交割。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">该负责人表示，新的晚籼稻期货基准交割品指标主要参照黄华占稻谷设计，替代品指标则参照两优系列稻谷设计，上述两个品种均为市场中种植面积较大的优质稻谷品种。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">市场人士普遍认为，此次修订符合产业发展趋势，修订后的晚籼稻期货交割标的物定位更加清晰，能够较好满足产业的实际需求，有助于晚籼稻期货功能进一步发挥。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">如何保证交割标的物的“品种优质”？上述负责人表示，郑商所收集了近200份优质稻谷样品，对稻谷品种的指标特点进行了分析总结，同时参考《中华人民共和国国家标准优质稻谷》（GB/T17891-2017）内容，对交割指标体系进行了调整优化。例如，保留长宽比指标，要求基准交割品长宽比大于3.1，替代品长宽比在2.8和3.1之间，并根据该指标设置升贴水，突出“优质优价”原则；用垩白度指标替换了垩白粒率指标，要求参与交割的晚籼稻垩白度不高于2%，保证交割品感官指标的“优质”性；增加并设定异品种率不得高于7%，防止掺混较为严重的晚籼稻入库交割。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">该负责人提到，在保证“品种优质”的同时，新的交割标准也收严了对储存品质的要求。根据新标准，每年10月1日至次年3月31日入库的晚籼稻，脂肪酸值不得高于17mg/100g（干基）；其他时间入库的晚籼稻，脂肪酸值不得高于19mg/100g（干基）。相同时间段内入库晚籼稻的脂肪酸值较原标准分别降低了2mg/100g（干基）、3mg/100g（干基），入库晚籼稻的新鲜度较之前更好。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">此外，为贴合优质稻谷的加工需求，新交割标准将水分含量由原来的不高于13.5%修订为不高于14.5%，每年10月1日至<span style="">次年3月31日入库的晚籼稻，水分含量在14.5%和15.5%之间的，可扣量入库。考虑到当前晚籼稻机械化收割和烘干的现状，新交割标准将谷外糙米含量由不高于2%修订为不高于4%。</span></span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">据介绍，由于基准交割品参照物黄华占和替代品参照物两优系列稻谷的价差不稳定，今后将以公告的方式发布升贴水，最新发布的替代品贴水幅度为190元/吨。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">上述负责人表示，此次规则修订主要集中在交割标准的调整，交割方式，限仓标准等内容均未进行调整。</span>
					</p>
					<p align="justify">
						<strong><span style="font-family:SimSun;font-size:14px;">转载声明</span></strong><span style="font-family:SimSun;font-size:14px;">：转载文章仅为传播更多信息之目的，并不代表本网站赞同其观点，本网站亦不保证文章内容的真实性、准确性和可靠性。文章内容仅供参考，并不构成任何投资建议及入市依据，且不因接收人收到此内容而视其为客户。凡据此入市者，风险和责任需由使用者自行承担。如果本网站转载的文章不符合作者的版权声明或者作者不希望转载文章的。</span> 
					</p>
									</div>` },
				{ id:2, title:'上期所公布铝期货和锌期货合约上期所公布铝期货和锌期货合约', author:'平台', updateTime:'2022-01-30', imgs:'https://img1.baidu.com/it/u=1399456712,4106567011&fm=253&fmt=auto&app=120&f=PNG?w=735&h=500',html: `<div class="details">
											
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">随着居民生活水平不断提高，市场对优质稻米的需求也随之增加，越来越多的优质稻品种涌向市场，“普改优”已成为稻米产业种植结构调整的重要方向。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">优质晚籼稻是加工小包装商品米所需的主要原料，其价格波动会给企业造成较大的生产经营风险。为更好满足企业的加工和套期保值需求，为企业提供有效的风险管理工具，2020年7月份，郑商所对晚籼稻期货交割标准进行了修订。</span> 
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">日前，郑商所相关负责人介绍，此次交割标准修订主要内容为：一是优化交割指标体系，将期货交割标的物定位于优质晚籼稻；二是调整替代交割品贴水幅度，充分体现“优质优价”原则；三是收严入库储存品质判定指标，避免储存品质较差的晚籼稻参与交割。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">该负责人表示，新的晚籼稻期货基准交割品指标主要参照黄华占稻谷设计，替代品指标则参照两优系列稻谷设计，上述两个品种均为市场中种植面积较大的优质稻谷品种。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">市场人士普遍认为，此次修订符合产业发展趋势，修订后的晚籼稻期货交割标的物定位更加清晰，能够较好满足产业的实际需求，有助于晚籼稻期货功能进一步发挥。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">如何保证交割标的物的“品种优质”？上述负责人表示，郑商所收集了近200份优质稻谷样品，对稻谷品种的指标特点进行了分析总结，同时参考《中华人民共和国国家标准优质稻谷》（GB/T17891-2017）内容，对交割指标体系进行了调整优化。例如，保留长宽比指标，要求基准交割品长宽比大于3.1，替代品长宽比在2.8和3.1之间，并根据该指标设置升贴水，突出“优质优价”原则；用垩白度指标替换了垩白粒率指标，要求参与交割的晚籼稻垩白度不高于2%，保证交割品感官指标的“优质”性；增加并设定异品种率不得高于7%，防止掺混较为严重的晚籼稻入库交割。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">该负责人提到，在保证“品种优质”的同时，新的交割标准也收严了对储存品质的要求。根据新标准，每年10月1日至次年3月31日入库的晚籼稻，脂肪酸值不得高于17mg/100g（干基）；其他时间入库的晚籼稻，脂肪酸值不得高于19mg/100g（干基）。相同时间段内入库晚籼稻的脂肪酸值较原标准分别降低了2mg/100g（干基）、3mg/100g（干基），入库晚籼稻的新鲜度较之前更好。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">此外，为贴合优质稻谷的加工需求，新交割标准将水分含量由原来的不高于13.5%修订为不高于14.5%，每年10月1日至<span style="">次年3月31日入库的晚籼稻，水分含量在14.5%和15.5%之间的，可扣量入库。考虑到当前晚籼稻机械化收割和烘干的现状，新交割标准将谷外糙米含量由不高于2%修订为不高于4%。</span></span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">据介绍，由于基准交割品参照物黄华占和替代品参照物两优系列稻谷的价差不稳定，今后将以公告的方式发布升贴水，最新发布的替代品贴水幅度为190元/吨。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">上述负责人表示，此次规则修订主要集中在交割标准的调整，交割方式，限仓标准等内容均未进行调整。</span>
					</p>
					<p align="justify">
						<strong><span style="font-family:SimSun;font-size:14px;">转载声明</span></strong><span style="font-family:SimSun;font-size:14px;">：转载文章仅为传播更多信息之目的，并不代表本网站赞同其观点，本网站亦不保证文章内容的真实性、准确性和可靠性。文章内容仅供参考，并不构成任何投资建议及入市依据，且不因接收人收到此内容而视其为客户。凡据此入市者，风险和责任需由使用者自行承担。如果本网站转载的文章不符合作者的版权声明或者作者不希望转载文章的。</span> 
					</p>
									</div>` },
			],//内容1
			
			contTwoList:[
				{ id:1, imgs:'https://img2.baidu.com/it/u=1484456337,1126487471&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=309', name:'【媒体看期市】郑商所发布花生期货合约及相关业务规则', money:'', yu:'' ,html: `<div class="details">
											
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">随着居民生活水平不断提高，市场对优质稻米的需求也随之增加，越来越多的优质稻品种涌向市场，“普改优”已成为稻米产业种植结构调整的重要方向。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">优质晚籼稻是加工小包装商品米所需的主要原料，其价格波动会给企业造成较大的生产经营风险。为更好满足企业的加工和套期保值需求，为企业提供有效的风险管理工具，2020年7月份，郑商所对晚籼稻期货交割标准进行了修订。</span> 
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">日前，郑商所相关负责人介绍，此次交割标准修订主要内容为：一是优化交割指标体系，将期货交割标的物定位于优质晚籼稻；二是调整替代交割品贴水幅度，充分体现“优质优价”原则；三是收严入库储存品质判定指标，避免储存品质较差的晚籼稻参与交割。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">该负责人表示，新的晚籼稻期货基准交割品指标主要参照黄华占稻谷设计，替代品指标则参照两优系列稻谷设计，上述两个品种均为市场中种植面积较大的优质稻谷品种。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">市场人士普遍认为，此次修订符合产业发展趋势，修订后的晚籼稻期货交割标的物定位更加清晰，能够较好满足产业的实际需求，有助于晚籼稻期货功能进一步发挥。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">如何保证交割标的物的“品种优质”？上述负责人表示，郑商所收集了近200份优质稻谷样品，对稻谷品种的指标特点进行了分析总结，同时参考《中华人民共和国国家标准优质稻谷》（GB/T17891-2017）内容，对交割指标体系进行了调整优化。例如，保留长宽比指标，要求基准交割品长宽比大于3.1，替代品长宽比在2.8和3.1之间，并根据该指标设置升贴水，突出“优质优价”原则；用垩白度指标替换了垩白粒率指标，要求参与交割的晚籼稻垩白度不高于2%，保证交割品感官指标的“优质”性；增加并设定异品种率不得高于7%，防止掺混较为严重的晚籼稻入库交割。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">该负责人提到，在保证“品种优质”的同时，新的交割标准也收严了对储存品质的要求。根据新标准，每年10月1日至次年3月31日入库的晚籼稻，脂肪酸值不得高于17mg/100g（干基）；其他时间入库的晚籼稻，脂肪酸值不得高于19mg/100g（干基）。相同时间段内入库晚籼稻的脂肪酸值较原标准分别降低了2mg/100g（干基）、3mg/100g（干基），入库晚籼稻的新鲜度较之前更好。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">此外，为贴合优质稻谷的加工需求，新交割标准将水分含量由原来的不高于13.5%修订为不高于14.5%，每年10月1日至<span style="">次年3月31日入库的晚籼稻，水分含量在14.5%和15.5%之间的，可扣量入库。考虑到当前晚籼稻机械化收割和烘干的现状，新交割标准将谷外糙米含量由不高于2%修订为不高于4%。</span></span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">据介绍，由于基准交割品参照物黄华占和替代品参照物两优系列稻谷的价差不稳定，今后将以公告的方式发布升贴水，最新发布的替代品贴水幅度为190元/吨。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">上述负责人表示，此次规则修订主要集中在交割标准的调整，交割方式，限仓标准等内容均未进行调整。</span>
					</p>
					<p align="justify">
						<strong><span style="font-family:SimSun;font-size:14px;">转载声明</span></strong><span style="font-family:SimSun;font-size:14px;">：转载文章仅为传播更多信息之目的，并不代表本网站赞同其观点，本网站亦不保证文章内容的真实性、准确性和可靠性。文章内容仅供参考，并不构成任何投资建议及入市依据，且不因接收人收到此内容而视其为客户。凡据此入市者，风险和责任需由使用者自行承担。如果本网站转载的文章不符合作者的版权声明或者作者不希望转载文章的。</span> 
					</p>
									</div>`},
				{ id:2, imgs:'https://img0.baidu.com/it/u=3284388619,708735942&fm=253&fmt=auto&app=120&f=JPEG?w=550&h=342', name:'原标题：机构投资策略“解局”： 大宗商品高涨黄金逆势低迷 比特币争宠', money:'', yu:'',html: `<div class="details">
											
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">随着居民生活水平不断提高，市场对优质稻米的需求也随之增加，越来越多的优质稻品种涌向市场，“普改优”已成为稻米产业种植结构调整的重要方向。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">优质晚籼稻是加工小包装商品米所需的主要原料，其价格波动会给企业造成较大的生产经营风险。为更好满足企业的加工和套期保值需求，为企业提供有效的风险管理工具，2020年7月份，郑商所对晚籼稻期货交割标准进行了修订。</span> 
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">日前，郑商所相关负责人介绍，此次交割标准修订主要内容为：一是优化交割指标体系，将期货交割标的物定位于优质晚籼稻；二是调整替代交割品贴水幅度，充分体现“优质优价”原则；三是收严入库储存品质判定指标，避免储存品质较差的晚籼稻参与交割。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">该负责人表示，新的晚籼稻期货基准交割品指标主要参照黄华占稻谷设计，替代品指标则参照两优系列稻谷设计，上述两个品种均为市场中种植面积较大的优质稻谷品种。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">市场人士普遍认为，此次修订符合产业发展趋势，修订后的晚籼稻期货交割标的物定位更加清晰，能够较好满足产业的实际需求，有助于晚籼稻期货功能进一步发挥。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">如何保证交割标的物的“品种优质”？上述负责人表示，郑商所收集了近200份优质稻谷样品，对稻谷品种的指标特点进行了分析总结，同时参考《中华人民共和国国家标准优质稻谷》（GB/T17891-2017）内容，对交割指标体系进行了调整优化。例如，保留长宽比指标，要求基准交割品长宽比大于3.1，替代品长宽比在2.8和3.1之间，并根据该指标设置升贴水，突出“优质优价”原则；用垩白度指标替换了垩白粒率指标，要求参与交割的晚籼稻垩白度不高于2%，保证交割品感官指标的“优质”性；增加并设定异品种率不得高于7%，防止掺混较为严重的晚籼稻入库交割。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">该负责人提到，在保证“品种优质”的同时，新的交割标准也收严了对储存品质的要求。根据新标准，每年10月1日至次年3月31日入库的晚籼稻，脂肪酸值不得高于17mg/100g（干基）；其他时间入库的晚籼稻，脂肪酸值不得高于19mg/100g（干基）。相同时间段内入库晚籼稻的脂肪酸值较原标准分别降低了2mg/100g（干基）、3mg/100g（干基），入库晚籼稻的新鲜度较之前更好。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">此外，为贴合优质稻谷的加工需求，新交割标准将水分含量由原来的不高于13.5%修订为不高于14.5%，每年10月1日至<span style="">次年3月31日入库的晚籼稻，水分含量在14.5%和15.5%之间的，可扣量入库。考虑到当前晚籼稻机械化收割和烘干的现状，新交割标准将谷外糙米含量由不高于2%修订为不高于4%。</span></span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">据介绍，由于基准交割品参照物黄华占和替代品参照物两优系列稻谷的价差不稳定，今后将以公告的方式发布升贴水，最新发布的替代品贴水幅度为190元/吨。</span>
					</p>
					<p style="text-align:justify;">
						<span style="font-size:14px;font-family:SimSun;">上述负责人表示，此次规则修订主要集中在交割标准的调整，交割方式，限仓标准等内容均未进行调整。</span>
					</p>
					<p align="justify">
						<strong><span style="font-family:SimSun;font-size:14px;">转载声明</span></strong><span style="font-family:SimSun;font-size:14px;">：转载文章仅为传播更多信息之目的，并不代表本网站赞同其观点，本网站亦不保证文章内容的真实性、准确性和可靠性。文章内容仅供参考，并不构成任何投资建议及入市依据，且不因接收人收到此内容而视其为客户。凡据此入市者，风险和责任需由使用者自行承担。如果本网站转载的文章不符合作者的版权声明或者作者不希望转载文章的。</span> 
					</p>
									</div>` },
			]
		}
	},
	onLoad() {
		 
	},
	created() {
		this.newsListData = this.newsListdatas.slice(0, 5)
	},
	methods: {
		//官网复制的轮播
		changeIndicatorDots(e) {
			this.indicatorDots = !this.indicatorDots
		},
		changeAutoplay(e) {
			this.autoplay = !this.autoplay
		},
		intervalChange(e) {
			this.interval = e.target.value
		},
		durationChange(e) {
			this.duration = e.target.value
		},
		lengmen(symbol) {
			uni.navigateTo({
				url: '/pages/SecView/lineDetail?item='+ encodeURIComponent(JSON.stringify(symbol))
			})
		},
		lengmenmore() {
			uni.navigateTo({
				url:'../ThrView/fhrview'
			})
		},
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
		swiperclick() {
			uni.navigateTo({
				url: '/pages/ThrView/hotnewsdetail?item='+ encodeURIComponent(JSON.stringify(this.contTwoList[0]))
			});
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
			.swiper{  height: 307rpx; }
			.swiper-item image{ width: 100%;height: 307rpx;display: block; }
			
			.idxMain{ width: 100%;padding-top: 100upx; }
			.idxMainBox{ width: 92%;margin: 0 auto; }
			.contBg{ background: #FFFFFF;overflow: hidden;margin-bottom: 30upx; }
			
			.contOver{ border-bottom: 1px #EDEDED solid;overflow: hidden;transition: all 0.4s; }
			.contOver:active{ background: #E2E2E2; }
			.contOver:last-child{ border-bottom: none; }
			.contOverLt{ float: left;width: 60%; }
			.contTxt{
				color: #333333;
				font-size: 30upx;
				width: 100%;
				text-overflow: ellipsis;
				display: -webkit-box;
				-webkit-line-clamp:2;
				-webkit-box-orient:vertical;
				overflow: hidden;
				padding-top: 30upx;
			}
			.contTime{ color: #888888;font-size: 24upx;margin-top: 30upx;margin-left: -130upx; }
			.contRtImg{ float: left;width:40%;height: 155upx;margin: 30upx 0; }
			.contRtImg image{ width: 100%;height: 100%;display: block;border-radius: 6upx; }
			
			.contTitle{ background: #FFFFFF;font-size: 30upx;color: #3B7ED5;height: 80upx;line-height: 80upx;border-bottom: 1px #F5F5F5 solid; }
			.shopOver{ overflow: hidden;margin-bottom: 30upx; }
			.shopLt{ 
				float: left;
				width: 48.5%;
				background: #FFFFFF;
				height: 360upx;
				border: 1px #F2F2F2 solid;
				border-radius: 12upx;
				transition: all 0.4s;
				margin-top: 15upx;
			}
			.shopLt:nth-child(2n){ float: right; }
			.shopLt:active{ background: #E2E2E2; }
			.shopImg{ height: 220upx; }
			.shopImg image{ width: 100%;height: 100%;display: block;border-radius: 12upx 12upx 0 0; }
			.shopTxt{ font-size: 28upx;color: #333333;padding: 20upx 20upx 0 20upx;display:block;white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
			.shopMoney{ padding: 0 20upx; }
			.shopMoney text{ font-size: 26upx;color: red; }
			.shopMoney text:last-child{ color: #aaaaaa; }
			
			.newsOver{ border-bottom: 1px #F5F5F5 solid;transition: all 0.4s; }
			.newsOver:active{ background: #E2E2E2; }
			.newsOver:last-child{ border-bottom: none; }
			.newsTitle{ 
				font-size: 30upx;
				color: #333333;
				text-overflow: ellipsis;
				display: -webkit-box;
				-webkit-line-clamp:3;
				-webkit-box-orient:vertical;
				overflow: hidden;
				padding: 30upx 0 20upx 0;
				text-align: justify;
			}
			.newsImg{ height: 360upx;border: 1px #F5F5F5 solid; }
			.newsImg image{ width: 100%;height: 100%;display: block; }
			.newsTime{ overflow: hidden;padding: 20upx 0 30upx 0; }
			.newsTime text{ font-size: 26upx;color: #AAAAAA;float: left; }
			.newsTime text:last-child{ float: right; }
		}
		.scrolllist {
			margin: 0 15px;
			.scroll-list {
				@include flex(column);
			
				&__goods-item {
					margin-right: 20px;
					background-color: #efefef;
					position: relative;
					&__image {
						position: absolute;
						top: 0px;
						right: 0px;
						width: 28px;
						height: 28px;
						
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
