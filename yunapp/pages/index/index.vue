<template>
	<view class="box">
		<commonList :list="list"></commonList>
	</view>
</template>

<script setup>
	import  commonList  from "../../components/common/common-list.vue"
	const list = [{
			avatar: '../../static/logo.png',
			nikeName: 'wqeqwe',
			time: '2019-10-12',
			title: '我是标题',
			titlePic: '../../static/tabBar/msg.png',
			support: {
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
			titlePic: '../../static/tabBar/msg.png',
			support: {
				support_num: 1,
				unsupport_num: 2
			},
			comment_num: 2,
			share_num: 3
		}
	]
</script>

<style lang="scss">
	.box {
		
	}
</style>