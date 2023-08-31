<template>
	<view class="topic-list" @click="goToDetail(topicItem)">
		<image :src="topicItem.img" style="width:150rpx; height: 150rpx;
					border-radius: 20rpx;"></image>
					<view class="info">
						<view>
							#<text class="title">{{topicItem.title}}</text>#
						</view>
						<view class="">
							{{topicItem.desc}}
						</view>
						<view >
							<text style="margin-right: 20rpx;">动态:{{topicItem.news_count}}</text>
							<text>今日:{{topicItem.today_count}}</text>
						</view>
					</view>
	</view>
</template>

<script setup>
	import { defineProps,defineEmits } from "vue"
		defineProps({
			topicItem:{
				type:Object,
				default:()=>{}
			},
		})
		const goToDetail=(topicItem)=>{
			uni.navigateTo({
				url:'../../pages/topic-detail/topic-detail?detail='+JSON.stringify(topicItem)
			})
		}
</script>

<style lang="scss">
	.topic-list
	{
		margin: 20rpx 20rpx;
		display: flex;
		.info
		{
			margin-left: 20rpx;
			padding: 10rpx 0;
			.title
			{
				font-size: 40rpx;
				font-weight: bold;
			}
		}
	}
</style>