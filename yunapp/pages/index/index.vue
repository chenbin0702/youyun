<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<text class="iconfont icon-QQ"></text>
		<text class="iconfont icon-bianji1"></text>
	</view>
</template>

<script setup>
 const title='标题'
 const handle=()=>
 {
	 console.log("sadas");
 }
</script>

<style>

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
