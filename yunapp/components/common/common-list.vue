<template>
	<view class="list">
		<!-- 头像|昵称|关注 -->
		<view class="list-item" v-for="(item,index) in list" :key="index">
			<view class="item-top">
				<view class="avatar-box">
					<!-- 头像-->
					<view class="avatar">
						<image :src="item.avatar"></image>
					</view>
					<!-- 昵称|时间 -->
					<view class="nike-time">
						<view>
							{{item.nikeName}}
						</view>
						<text>{{item.time}}</text>
					</view>
				</view>
				<!-- 关注 -->
				<view class="follow">
					关注
				</view>
	
			</view>
			<!-- 标题 -->
			<view class="title">
				{{item.title}}
			</view>
			<!-- 图片 -->
			<view class="">
				<image :src="item.titlePic" mode="" style="height: 300rpx;"></image>
			</view>
			
			<!-- 图标按钮 -->
			<view style="display: flex;">
				<view class="icon-item">
					<view class="iconfont icon-dianzan1" style="margin-right: 20rpx;">
			
					</view>
					<text>{{item.support.support_num}}</text>
				</view>
				<view class="icon-item">
					<view class="iconfont icon-cai" style="margin-right: 20rpx;">
			
					</view>
					<text>{{item.support.unsupport_num}}</text>
				</view>
				<view class="icon-item">
					<view class="iconfont icon-pinglun2" style="margin-right: 20rpx;">
			
					</view>
					<text>{{item.comment_num}}</text>
				</view>
				<view class="icon-item">
					<view class="iconfont icon-fenxiang" style="margin-right: 20rpx;">
			
					</view>
					<text>{{item.share_num}}</text>
				</view>
			</view>
		</view>
		
		
	</view>
</template>

<script setup>
	import { defineProps } from "vue"
	defineProps({
		list:{
			type:Array,
			default:()=>[]
		}
	})
</script>

<style lang="scss">
	.list {
		padding: 20rpx;
		.list-item {
			 margin-bottom: 40rpx;
			.item-top {
				display: flex;
				justify-content: space-between;
				align-items: center;
	            margin-bottom: 10rpx;
				.avatar-box {
					display: flex;
					align-items: center;
	
					.avatar {
						width: 70rpx;
						height: 70rpx;
						margin-right: 20rpx;
	
						image {
							width: 100%;
							height: 100%;
							border-radius: 100%;
						}
					}
	
					.nike-time {
						text {
							color: #9D9589;
						}
					}
				}
	
				.follow {
					width: 90rpx;
					height: 50rpx;
					display: flex;
					align-items: center;
					justify-content: center;
					border-radius: 10rpx;
					background-color: #fd597c;
					color: #ffffff;
				}
	
			}
	
		}
	}
	
	.icon-item {
		display: flex;
		flex: 1;
		justify-content: center;
	}
</style>