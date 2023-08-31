<template>
	<view>
		<u-navbar :placeholder="true" leftIcon="">
			<template #center>
				<view class="navbar-center">
					<text class="tabTitle" v-for="(item,index) in tabBarItem" :key="index" @click="changeTabItem(index)"
						:class="tabIndex===index?'active':''">{{item.name}}</text>
				</view>

			</template>
			<template #right>
				<u-icon name="edit-pen" size="50" @click="eidtInput"></u-icon>
			</template>
		</u-navbar>
		<swiper :duration="150" :style="{height:scrollH+'px'}" :current="tabIndex" @change="onChangeTab">
			<swiper-item>
				<scroll-view scroll-y :style="{height:scrollH+'px'}">
					<commonList :list="list" @doSupport="doSupport"></commonList>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<!-- 热门分类 -->
				<hotCate :tags="tags"></hotCate>
				<!-- 搜索框 -->
				<view class="search">
					<u-search :show-action="true" actionText="搜索" height="72" searchIconSize="40"
						:animation="true"></u-search>
				</view>
				<!-- 轮播图 -->
				<view class="uni-margin-wrap">
					<swiper class="swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
						<swiper-item>
							<image src='../../static/Snipaste_2023-07-17_09-08-30.png'
								style="height: 300rpx; width: 100%; border-radius: 20rpx;"></image>
						</swiper-item>
						<swiper-item>
							<image src='../../static/logo.png'
								style="height: 300rpx; width: 100%; border-radius: 20rpx;"></image>
						</swiper-item>
					</swiper>
				</view>
			 <!-- 最近更新 -->
			 <view style="margin: 0 20rpx;">
			 	最近更新
			 </view>
			<block v-for="(item,index) in TopicList" :key="index">
				<topicList :topicItem="item"></topicList>
			</block>
			
			 </swiper-item>
		</swiper>
	</view>
</template>

<script setup>
	import {
		onLoad,
		onNavigationBarSearchInputClicked,
		onNavigationBarButtonTap
	} from '@dcloudio/uni-app'
	import commonList from "../../components/common/common-list.vue"
	import hotCate from "../../components/news/hot-cate.vue"
	import topicList from "../../components/news/topic-list.vue"
	import {
		reactive,
		ref
	} from "vue"
	const scrollH = ref(500)
	const list = reactive([{
			avatar: '../../static/logo.png',
			nikeName: 'wqeqwe',
			time: '2019-10-12',
			title: '我是标题',
			isFollow: true,
			titlePic: '',
			support: {
				type: 'support',
				support_num: 1,
				unsupport_num: 1
			},
			comment_num: 1,
			share_num: 0
		},
		{
			avatar: '../../static/logo.png',
			nikeName: '陈斌吃不吃',
			time: '2019-10-12',
			title: '我是标题',
			isFollow: true,
			titlePic: '../../static/tabBar/msg.png',
			support: {
				type: 'unsupport',
				support_num: 1,
				unsupport_num: 2
			},
			comment_num: 2,
			share_num: 3
		},
		{
			avatar: '../../static/logo.png',
			nikeName: '陈斌吃不吃',
			time: '2019-10-12',
			title: '我是标题',
			isFollow: true,
			titlePic: '../../static/tabBar/msg.png',
			support: {
				type: 'unsupport',
				support_num: 1,
				unsupport_num: 2
			},
			comment_num: 2,
			share_num: 3
		},

	])
	let tabIndex = ref(0)
	const TopicList=reactive([
		{
			img:'/static/logo.png',
			title:'今日话题',
			desc:'话题描述',
			today_count:0,
			news_count:10
		},
		{
			img:'/static/logo.png',
			title:'今日话题',
			desc:'话题描述',
			today_count:0,
			news_count:10
		},
	])
	const tags = reactive([{
			name: '关注'
		},
		{
			name: '推荐'
		},
		{
			name: '体育'
		},
		{
			name: '热点'
		},
		{
			name: '游戏'
		},
		{
			name: '娱乐'
		}
	]);
	const radioClick = (name) => {
		radios.forEach((item, index) => {
			item.checked = index === name;
		});
	};

	// 页面加载
	onLoad(() => {

		uni.getSystemInfo({
			success: (res) => {
				scrollH.value = res.windowHeight - res.statusBarHeight - 44
				console.log(scrollH.value);
			}
		})
	})
	const tabBarItem = reactive([{
			name: '关注'
		},
		{
			name: '话题'
		}
	])
	const changeTabItem = (index) => {
		tabIndex.value = index
	}
	const onChangeTab = (e) => {
		changeTabItem(e.detail.current)
	}
	const eidtInput = () => {
		uni.navigateTo({
			url: '../add-input/add-input',
		})
	}

	const doSupport = (data) => {
		let item = list[data.index]
		let msg = data.type === "support" ? "点赞" : "踩"
		// 之前没有操作过
		if (item.support.type === '') {
			item.support[data.type + '_num']++
		}
		// 之前是点赞 接下来是踩
		else if (item.support.type === 'support' && data.type === 'unsupport') {
			item.support.support_num--;
			item.support.unsupport_num++;
		}
		// 之前是踩 接下来是点赞
		else if (item.support.type === 'unsupport' && data.type === 'support') {
			item.support.support_num++;
			item.support.unsupport_num--;
		}
		// 之前是什么 接下来也是什么
		else if (item.support.type === data.type) {
			item.support.type = ''
			item.support[data.type + '_num']--
			uni.showToast({
				title: `取消${msg}`
			});
			return
		}
		item.support.type = data.type
		uni.showToast({
			title: `${msg}成功`
		});
	}
</script>

<style lang="scss" scoped>
	.navbar-center {
		display: flex;
		align-items: center;

		.tabTitle {
			margin-right: 10rpx;
			font-weight: bold;
			font-size: 36rpx;
			color: #ccc;
		}

		.active {
			font-weight: bold;
			font-size: 42rpx;
			color: hotpink;
		}
	}

	.search {
		margin: 20rpx 20rpx;
	}

	.swiper {
		margin: 20rpx 20rpx;
	}

</style>