<template>
	<view class="box">
		
		<view class="tabBar" >
			<scroll-view scroll-x class="scroll-row" 
			scroll-with-animation
			:scroll-into-view="scrollInfo">
				<view class="scroll-row-item" 
				v-for="(item,index) in tabBarList"
				 :key="index"
				:id="'tab'+index"
				:class="tabIndex===index?'active':''"
				@click="changeIndex(index)"
				>
					{{item.name}}
				</view>
			</scroll-view>
		</view>
		<swiper :currentIndex="tabIndex"  :duration="150"
		@change="changeSwiperIndex"
		:style="{height:scrollH+'px'}">
			<swiper-item v-for="(item,index) in tabBarList" :key="index"
			>
				<scroll-view scroll-y :style="{height:scrollH+'px'}">
			<!-- 	列表 -->
						<commonList :list="list"
						 @follow="follow"
						 @doSupport="doSupport"
						></commonList>
				
				</scroll-view>
			</swiper-item>
		</swiper>
	
	</view>
	
</template>

<script setup>
	import {reactive,ref} from 'vue';	
	import { onLoad, onShow } from '@dcloudio/uni-app'
	import  commonList  from "../../components/common/common-list.vue"

	const scrollH=ref(0)
	const tabIndex=ref(0)
	const scrollInfo=ref("tab0")
	const tabBarList=[{name:'关注'},{
		name:'推荐',
		},
		{
			name:'体育'
		},
		{
			name:'热点'
		},
		{
			name:'财经'
		},
		{
			name:'娱乐'
		},
		{
			name:'历史'
		},
		{
			name:'政治'
		},
		]
	const list =reactive([{
			avatar: '../../static/logo.png',
			nikeName: 'wqeqwe',
			time: '2019-10-12',
			title: '我是标题',
			isFollow:false,
			titlePic: '',
			support: {
				type:'support',
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
			isFollow:false,
			titlePic: '../../static/tabBar/msg.png',
			support: {
				type:'unsupport',
				support_num: 1,
				unsupport_num: 2
			},
			comment_num: 2,
			share_num: 3
		}
	]) 
	// 页面加载
	onLoad(()=>{
		uni.getSystemInfo({
			success: (res) => {
				scrollH.value=res.windowHeight-uni.upx2px(100)
				console.log(scrollH.value);
			}
		})
	})
	// 获取数据
	const getData=()=>{
	    
	}
	// 关注
	const follow=(e)=>{
		list[e].isFollow=true
		console.log(list[e].isFollow);
		uni.showToast({title:"关注成功"})
	}
	// 改变tabBar 索引
	const changeIndex=(index)=>{
		// console.log(tabIndex.value);
		if(tabIndex.value===index) return
		tabIndex.value=index
		scrollInfo.value='tab'+index
	}
	// 滑动改变index
	const changeSwiperIndex=(e)=>{
		changeIndex(e.detail.current)
	}
	const doSupport=(data)=>{
		let item=list[data.index]
		let msg=data.type==="support"?"点赞":"踩"
		// 之前没有操作过
		if(item.support.type==='')
		{
			item.support[data.type+'_num']++
		}
		// 之前是点赞 接下来是踩
		else if(item.support.type==='support'&&data.type==='unsupport')
		{
			item.support.support_num--;
			item.support.unsupport_num++;
		}
		// 之前是踩 接下来是点赞
		else if(item.support.type==='unsupport'&&data.type==='support')
		{
			item.support.support_num++;
			item.support.unsupport_num--;
		}
		// 之前是什么 接下来也是什么
		else if(item.support.type===data.type)
		{
			item.support.type=''
			item.support[data.type+'_num']--
			uni.showToast({
				title: `取消${msg}`
			});
			return
		}
		item.support.type=data.type
		uni.showToast({
			title: `${msg}成功`
		});
	}
</script>

<style lang="scss">
	.box {
		
		.tabBar
		{
			margin-top: 20rpx;
			.scroll-row
			{
				width: 100%;
				white-space: nowrap;
				height: 100rpx;
				border-bottom: 2px solid #ccc;
				.scroll-row-item
				{
					font-size: 30rpx;
					padding: 20rpx 40rpx;
					display: inline-block!important;
				}
			}
			.active
			{
				font-size: 40rpx !important;
				color: hotpink;
				font-weight: bold;
			}
		}
	
	}
</style>