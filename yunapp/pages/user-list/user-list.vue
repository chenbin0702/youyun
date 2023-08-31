<template>
	<view>
		<view class="navbar-center">
			<text class="tabTitle" v-for="(item,index) in tabBarItem" :key="index" @click="changeTabItem(index)"
				:class="tabIndex===index?'active':''">
				<text>{{item.name}}</text>
				<text v-if="item.num>0">{{item.num}}</text>
			</text>
		</view>
		<swiper :current="tabIndex" :duration="150" @change="changeSwiperIndex" :style="{height:scrollH+'px'}">
			<swiper-item v-for="(item,index) in newList" :key="index">
				<scroll-view scroll-y :style="{height:scrollH+'px'}">
					<!-- 	列表 -->
					<template v-if="item.list.length>0">
						<block v-for="(item1,index) in item.list" :key="index">
                          <userList :info="item1"></userList>
						</block>
					</template>
					<template v-else>
						没有
					</template>
				</scroll-view>

			</swiper-item>
		</swiper>
	</view>
</template>

<script setup>
	import userList from "../../components/user/user-list.vue"
	import {
		reactive,
		ref
	} from "vue"
	import {
		onLoad,
		onNavigationBarSearchInputClicked,
		onNavigationBarButtonTap
	} from '@dcloudio/uni-app'
	const scrollH = ref(0)
	let newList = []
	const tabBarItem = reactive([{
			name: '互关',
			num: 0
		},
		{
			name: '关注',
			num: 10
		}, {
			name: '粉丝',
			num: 20
		}
	])
	let tabIndex = ref(0)
	onLoad(() => {
		getData()
		console.log(newList);
		uni.getSystemInfo({
			success: (res) => {
				scrollH.value = res.windowHeight - uni.upx2px(100)
				console.log(scrollH.value);
			}
		})
	})
	const getData = () => {
		const arr = []
		for (let i = 0; i < tabBarItem.length; i++) {
			let obj = {
				list: [{
						avatar: '../../static/logo.png',
						name: '陈斌',
						sex: '1',
						age: 21,
						follow: true
					},
					{
						avatar: '../../static/logo.png',
						name: '阳丹',
						sex: '0',
						age: 20,
						follow: false
					},
					{
						avatar: '../../static/logo.png',
						name: '单独',
						sex: '1',
						age: 10,
						follow: false
					},

				]
			}
			if (i > 3) {
				obj.list = []
			}
			arr.push(obj)
		}
		newList = reactive(arr)
	}
	onNavigationBarSearchInputClicked(() => {
		uni.navigateTo({
			url: '../search/search'
		})
	})
	onNavigationBarButtonTap(() => {
		uni.navigateBack({
			delta: 1
		})
	})
	const changeTabItem = (index) => {
		tabIndex.value = index
	}
	// 滑动改变index
	const changeSwiperIndex = (e) => {
		changeTabItem(e.detail.current)
	}
</script>

<style lang="scss">
	.navbar-center {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin: 0 20rpx;

		.tabTitle {
			padding: 0;
			font-weight: 600;
			font-size: 36rpx;
		}

		.active {
			font-weight: bold;
			font-size: 42rpx;
			color: hotpink;
		}
	}
</style>