<template>
	<view class="msg-list" @click="open">
		<view class="avatar">
			<up-avatar :src="info.avatar" :size="70"></up-avatar>
		</view>
		<view class="right">
			<view class="top-name">
				<text>{{info.nikename}}</text>
				<text style="font-size: 26rpx; color: #ccc; font-weight: 500;">{{Time.gettime(info.time)}}</text>
			</view>
			<view class="msg">
				<text class="content">{{info.content}}</text>
				<view> <up-badge max="99" :value="info.msg_num"></up-badge></view>
			</view>
		</view>
	</view>


</template>

<script setup>
	import Time from '../../common/time.js'
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
	const open=()=>{
		uni.navigateTo({
			url:'../../pages/user-chat/user-chat'
		})
	}
</script>

<style lang="scss">
	.msg-list {
		display: flex;
		height: 120rpx;
		align-items: center;
		margin: 10rpx;
		border-bottom: 1rpx solid #ccc;

		.right {
			display: flex;
			flex-direction: column;
			margin-left: 25rpx;
			width: 100%;
			padding: 20rpx 0;

			.top-name {
				display: flex;
				margin-bottom: 10rpx;
				width: 100%;
				justify-content: space-between;
			}

			.msg {
				display: flex;
				width: 100%;
				align-items: center;
				justify-content: space-between;

				.content {
					overflow: hidden;
					text-overflow: ellipsis;
					white-space: nowrap;
					max-lines: 1;
					max-width: 500rpx;
				}
			}
		}
	}
</style>