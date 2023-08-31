<template>
	<view class="user-list">
		<view class="avatar">
			<up-avatar :src="info.avatar" :size="80"></up-avatar>
		</view>
		<view class="msg">
			<view class="left">
				<view style="margin-bottom: 10rpx;">
					{{info.name}}
				</view>
				<view style="display: flex; align-items: center;">
					<text class="iconfont icon-nv" v-if="info.sex==='0'"></text>
					<text class="iconfont icon-nan" v-if="info.sex==='1'"></text>
					
					<up-badge :type="info.sex==='0'?'warning':'primary'" max="99" :value="info.age">

					</up-badge>
				</view>
			</view>
			
			<view class="right" >
				<u-icon name="checkmark-circle" :color="info.follow?'#cf697e':'#ccc'" size="40"></u-icon>
			</view>
		</view>
	</view>
</template>

<script setup>
	import {
		defineProps,
		defineEmits
	} from "vue"
	defineProps({
		info: {
			type: Object,
			default: () => {}
		},
	})
</script>

<style lang="scss" scoped>
	.user-list {
		height: 120rpx;
		display: flex;
		align-items: center;
		border-bottom: 1rpx solid #ccc;
		margin: 10rpx;
		width: 100%;

		.avatar {
			margin-right: 20rpx;
		}

		.msg {
			display: flex;
			width: 90%;
			justify-content: space-between;
			align-items: center;

			.right {
				margin-right: 40rpx;
			}
		}
	}
</style>