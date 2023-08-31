<template>
	<view>
		<view class="bottom-fixed">
			<view style="width: 90%; margin-right:10rpx;">
				<up-input
				    placeholder="请输入内容"
				    border="surround"
				    v-model="value"
				    @change="change"
					
				  ></up-input>
			</view>
		
			<view class="iconfont icon-fabu animate__animated" style="font-size: 45rpx;"
			hover-class="animate__jello">
				
			</view>
		</view>
	</view>
</template>

<script setup>

</script>

<style lang="scss" scoped>
.bottom-fixed
{
	position: fixed;
	right: 0;
	left: 0;
	bottom: 0;
	z-index: 1000;
	height: 100rpx;
	display: flex;
	align-items: center;
	margin: 0 10rpx;
	border-top: 1rpx solid lightgrey;
}
</style>
