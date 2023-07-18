<template>
	<view>
		<!-- 搜索历史 -->
		<template v-if="show">
			<view class="history">
				搜索历史
			</view>
			<view class="tag-box">
				<view class="tag-item" v-for="item in historyItem" :key="item" hover-class="light" @click="clickItem(item)">
					{{item}}
				</view>
			</view>
		</template>

		<!-- 数据列表 -->
		<template v-else>
			<commonList :list="searchList"></commonList>
		</template>
	</view>
</template>

<script setup>
	import {
		reactive,
		ref,
		nextTick
	} from 'vue';
	import commonList from "../../components/common/common-list.vue"
	import {
		onNavigationBarSearchInputChanged,
		onNavigationBarButtonTap,
		onShow
	} from '@dcloudio/uni-app'
 	
	
	const historyItem = reactive(['uniapp学习', 'vue3和vue2差别', 'node服务端知识', 'java学习', 'js高级', '陈斌哈哈挥挥'])
	let searchText = ref('')
	const demo = reactive([{
			avatar: '../../static/logo.png',
			nikeName: 'wqeqwe',
			time: '2019-10-12',
			title: '我是标题',
			isFollow: false,
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
			isFollow: false,
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
			isFollow: false,
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
	let searchList =reactive([])
    let show=ref(true)
	onNavigationBarSearchInputChanged((e) => {
		console.log(e);
		show.value=true
		searchText = e
	})
	// 触发搜索事件
	onNavigationBarButtonTap((e) => {
		if (e.index === 0) {
			searchEvent()
		}
	})
	// 搜索事件
	const searchEvent = () => {
		// 收起键盘
		uni.hideKeyboard()
		// 加载数据
		uni.showLoading({
			title: '加载中',
			mask: true
		})
	
			setTimeout(() => {
				// 隐藏加载中
				uni.hideLoading()
				searchList =demo
				nextTick(()=>{
					show.value=false
				})	
			}, 4000)
		
	}
	// 点击历史搜索
	const clickItem=(item)=>{
		searchText=item
		searchEvent()
	}
</script>


<style lang="scss">
	.history {
		margin: 20rpx;
	}

	.tag-box {
		display: flex;
		flex-wrap: wrap;

		.tag-item {
			border: 2rpx solid #ccc;
			margin: 10rpx 20rpx;
			border-radius: 10rpx;
			padding: 10rpx 20rpx;
			font-size: 24rpx;



		}

		.light {
			background-color: #f8f9fa;

		}

	}
</style>