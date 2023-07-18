<template>
	<view class="list">
		<!-- 头像|昵称|关注 -->
		<view class="list-item" v-for="(item,index) in list" :key="item">
			<view class="item-top">
				<view class="avatar-box">
					<!-- 头像-->
					<view class="avatar" @click="openSpace">
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
				<view class="follow animate__animated" hover-class="animate__heartBeat"
				@click="follow(index)"
				v-if="!item.isFollow">
					关注
				</view>
	
			</view>
			<!-- 标题 -->
			<view class="title">
				{{item.title}}
			</view>
			<!-- 图片 -->
			<view v-if="item.titlePic" @click="openDetail" class="img-box">
				<image :src="item.titlePic" mode="" style="height: 300rpx;"></image>
			</view>
			
			<!-- 图标按钮 -->
			<view style="display: flex; margin-bottom: 30rpx;">
				<view class="icon-item">
					<view 
					class="iconfont icon-dianzan2 animate__animated" 
					hover-class="animate__jello" 
					style="margin-right: 20rpx;"
			        :class="item.support.type === 'support'?'support-active':'' "
					@click="doSupport({type:'support',index})">
					</view>
					<text>{{item.support.support_num>0?item.support.support_num:"点赞"}}</text>
				</view>
				<view class="icon-item">
					<view class="iconfont icon-cai animate__animated" hover-class="animate__jello" style="margin-right: 20rpx;"
					 :class="item.support.type === 'unsupport'?'support-active':'' "
					 @click="doSupport({type:'unsupport',index})">
					</view>
					<text>{{item.support.unsupport_num>0?item.support.unsupport_num:'踩'}}</text>
				</view>
				<view class="icon-item">
					<view class="iconfont icon-pinglun2 animate__animated" hover-class="animate__jello"  style="margin-right: 20rpx;">
			
					</view>
					<text>{{item.comment_num>0?item.comment_num:'评论'}}</text>
				</view>
				<view class="icon-item">
					<view class="iconfont icon-fenxiang animate__animated" hover-class="animate__jello" style="margin-right: 20rpx;">
			
					</view>
					<text>{{item.share_num>0?item.share_num:'分享'}}</text>
				</view>
			</view>
		<divider></divider>
		</view>
		
	</view>
</template>

<script setup>
	import divider from "./divider.vue"
	import { defineProps,defineEmits } from "vue"
	defineProps({
		list:{
			type:Array,
			default:()=>[]
		},
	
	})
	const emit=defineEmits(['follow','doSupport'])
	// 个人空间
	const openSpace=()=>{
		console.log("openSpace");
	}
	// 关注
	const follow=(index)=>{
		emit('follow',index)
	}
	// 进入详情页
	const openDetail=()=>{
		
	}
	// 顶踩操作
	const doSupport=(data)=>{
		let newData={
			type:data.type,
			index:data.index
		}
	   emit('doSupport',newData)
	}
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
	        .title
			{
				margin-bottom: 20rpx;
			}
		}
	}
	.img-box
	{
		margin-bottom: 20rpx;
	}
	.icon-item {
		display: flex;
		flex: 1;
		font-size: 30rpx;
		align-items: center;
		justify-content: center;
	}
	.support-active
	{
		color: #fd597c;
	}
</style>