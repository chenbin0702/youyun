<template>
	<view class="">
		<view class="hot-cate">
			<text style="font-size: 28rpx;">热门分类</text>
			<view class="more" @click="moreCate">
				<text>更多</text>
				<u-icon name="arrow-right"></u-icon>
			</view>
		</view>
		<view class="tags">
			<view class="u-page__tag-item" v-for="(item, index) in tags" :key="index">
				<u-tag :text="`${item.name}`" type="info"  plain plainFill>
				</u-tag>
			</view>
		</view>
		
	</view>
</template>

<script setup>
import { defineProps,defineEmits } from "vue"
	defineProps({
		tags:{
			type:Array,
			default:()=>[]
		},
	})
	const moreCate=()=>{
		uni.navigateTo({
			url:'../../pages/topic-nav/topic-nav'
		})
	}
</script>

<style lang="scss">
	.hot-cate {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin: 10rpx 20rpx;
	
		.more {
			color: #ccc;
			display: flex;
			align-items: center;
		}
	}
	
	.tags {
		margin: 10rpx 20rpx;
		display: flex;
	
		.u-page__tag-item {
	
			margin-right: 20rpx;
		}
	}
</style>