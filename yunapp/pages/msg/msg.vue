<template>
	<view>
		<!-- 消息列表 -->
		<template v-if="list.length>0">
			<block v-for="(item,index) in list" :key="index">
				<msgList :info="item"></msgList>
			</block>
		</template>
	
		<template v-else>
			<u-empty
			        mode="list"
			        icon="http://cdn.uviewui.com/uview/empty/car.png"
			>
			</u-empty>
		</template>
		<!-- 顶部弹窗 -->
		   <u-transition :show="show">
		        <u-popup :show="show" mode="top"  @open="open" :closeable="true" :round="10" @close="close"
		          >
		                <view style="display: flex;justify-content: center;align-items: center;
		        		height: 150rpx; border-bottom: 1rpx solid #ccc;" class="hover">
		                   <u-icon name="search" color="#2979ff" size="40"></u-icon>
		        		   <text>搜索好友</text>
		                </view>
		        		<view style="display: flex;justify-content: center;align-items: center;
		        		height: 150rpx;">
		        		   <u-icon name="trash" color="#2979ff" size="40"></u-icon>
		        		   <text>清除列表</text>
		        		</view>
		        	</u-popup>
		    </u-transition>
	
	</view>
</template>

<script setup>
	import Time from '../../common/time.js'
	import msgList from "../../components/msg/msg-list.vue"
	import {
		reactive,
		ref
	} from "vue"
	import {
		onPullDownRefresh,
		onNavigationBarButtonTap
	} from '@dcloudio/uni-app'
	const show=ref(false)
	let list = reactive([{
			avatar: '../../static/logo.png',
			nikename: '陈斌',
			time: 1693358720,
			content: '唉唉唉唉唉唉i哎哎哎i爱爱i爱爱i哎i',
			msg_num: 10
		},
		{
			avatar: '',
			nikename: '阳丹',
			time: 1693358720,
			content: '唉唉唉唉唉唉i哎哎哎i爱爱i爱爱i哎i11111111',
			msg_num: 12
		}
	])
	const open=()=>{
		show.value=true
	}
	const close=()=>{
		show.value=false
	}
	onPullDownRefresh(() => {
		refresh()
	})
	const refresh = () => {
		let demo=list
		list=reactive([])
		setTimeout(() => {
			list=demo
			uni.stopPullDownRefresh()
		}, 2000)
	}
	onNavigationBarButtonTap((e)=>{
		switch(e.index)
		{
			case 0:
			uni.navigateTo({
				url:'../user-list/user-list'
			})
				break;
			case 1:
			   open()
			 break;
		}
	})
	
</script>

<style lang="scss">

</style>