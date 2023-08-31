<template>
	<view>
		<topicInfo :info="info"> </topicInfo>
		<divider></divider>
		<view class="notice" v-for="(item,index) in hotList" :key="index">
			<u-icon style="margin-right: 20rpx;" name="calendar" color="#2979ff" size="40"></u-icon>
			<text>{{item.title}}</text>
		</view>
		<divider></divider>
		<view style="display: flex;justify-content: center;">
			<u-tabs :list="tabList" lineWidth="30" lineColor="#f56c6c" :activeStyle="{
			            color: '#303133',
			            fontWeight: 'bold',
			            transform: 'scale(1.05)'
			        }" :inactiveStyle="{
			            color: '#606266',
			            transform: 'scale(1)'
			        }" itemStyle="padding-left: 15px; padding-right: 15px; height: 34px;"
					@click="changeTab"></u-tabs>
		</view>
        <template v-if="list.length>0"> 
			<commonList :list="list"></commonList>
		</template>
		<template v-else>
			<u-empty
			        mode="message"
			        icon="http://cdn.uviewui.com/uview/empty/message.png"
			>
			</u-empty>
		</template>
	</view>
</template>

<script setup>
	import topicInfo from "../../components/topic-detail/topic-info.vue"
	import divider from "../../components/common/divider.vue"
	import commonList from "../../components/common/common-list.vue"
	import {
		onLoad,
	} from '@dcloudio/uni-app'
	import {
		ref,
		reactive,
		computed
	} from "vue"
	let info = reactive({})
	onLoad((e) => {
		console.log(e);
		info = JSON.parse(e.detail)
	})
	const hotList = reactive([{
			title: '社交交友平台冲冲冲'
		},
		{
			title: '毕业设计 社交交友平台冲冲冲'
		}
	])
	const tabList = reactive([{
			name: '默认'
		},
		{
			name: '最新'
		}
	])
	let tabName=ref('默认')
	const normalList=reactive([{
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
					},])
	const newList=reactive([])
	let list=computed(()=>{
		if(tabName.value==='默认')
		{
			return normalList
		}
		else
		{
			return newList
		}
	})
	const changeTab=(e)=>{
		if(e.name==="默认")
		{
			tabName.value='默认'
		}
		else
		{
			tabName.value='最新'
		}
	}
</script>

<style lang="scss" scoped>
	.notice {
		display: flex;
		margin-left: 20rpx;
		height: 80rpx;
		align-items: center;
		border-bottom: 1rpx solid #ccc;
	}
</style>