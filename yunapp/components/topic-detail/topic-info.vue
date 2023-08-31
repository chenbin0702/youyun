<template>
	<view>
		<image src="https://img0.baidu.com/it/u=872183856,2147165038&fm=253&fmt=auto&app=138&f=JPEG?w=585&h=249" mode="aspectFill"
		style="height: 300rpx; width: 100%;" class="fliter"></image>
	</view>
	<view style="margin-left: 20rpx; margin-bottom: 10rpx;">
		<view style="display: flex;align-items: center;">
			<image :src="info.img" style="width:150rpx; height: 150rpx;
					border-radius: 20rpx;margin-top:-75rpx;">
			</image>
			<text style="margin-top:-45rpx;">#{{info.title}}#</text>
		</view>
		<view >
			<text style="margin-right: 20rpx;">动态:{{info.news_count}}</text>
			<text>今日:{{info.today_count}}</text>
		</view>
		<view class="">
			{{info.desc}}
		</view>
	</view>
</template>

<script setup>
	import { defineProps,defineEmits } from "vue"
		defineProps({
			info:{
				type:Object,
				default:()=>{}
			},
		})
</script>

<style lang="scss">
.fliter
{
	filter: blur(5rpx);
}
</style>
