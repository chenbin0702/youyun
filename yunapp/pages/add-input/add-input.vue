<template>
	<view class="add-input">
		<u-navbar :autoBack="true" :placeholder="true">
			<template #center>
				<view class="navbar-center">
					<text>所有人可见</text>
					<u-icon name="setting" size="32"></u-icon>
				</view>

			</template>
		</u-navbar>
		<view class="">
			<u--form labelPosition="left" :model="infoForm" labelWidth="auto">
				<u-form-item>
					<u--textarea v-model="infoForm.content" placeholder="说一句话吧" count border="bottom"
						height="150"></u--textarea>
				</u-form-item>
				<u-form-item label="图片">
					<u-upload :fileList="infoForm.imageList" @afterRead="afterRead" @delete="deletePic" ref="imageBox"
						:previewFullImage="true" name="1" deletable width="200" height="200" multiple
						:maxCount="9"></u-upload>
				</u-form-item>
			</u--form>
		</view>

		<view class="footer">
			<view class="footer-left">
				<u-icon name="grid" size="60" class="footer-icon"></u-icon>
				<u-icon name="share" size="60" class="footer-icon"></u-icon>
				<u-icon name="photo" size="60" @click="uploadImage"></u-icon>
			</view>
			<view class="footer-right">
				<up-button class="submit" type="primary">提交</up-button>
			</view>
		</view>
	</view>
</template>

<script setup>
	import {
		reactive,
		ref,
		getCurrentInstance
	} from "vue"
	import {
		onBackPress,
		onLoad
	} from '@dcloudio/uni-app'
	let infoForm = reactive({
		content: '',
		imageList: []
	})
	const instance = getCurrentInstance()
	const showBack = ref(false)
	// 页面加载
	onLoad(() => {
		uni.getStorage({
			key: 'add-input',
			success: (res) => {
				if (res.data) {
					let result = JSON.parse(res.data)
					infoForm = result
				}
			}
		})
	})
	// 保存数据
	const store = () => {
		console.log(infoForm);
		uni.setStorage({
			key: 'add-input',
			data: JSON.stringify(infoForm)
		})
	}
	// 监听返回
	onBackPress(() => {
		if ((infoForm.content !== '' || infoForm.imageList.length > 0) && !showBack.value) {
			uni.showModal({
				content: '是否要保存为草稿',
				showCancel: true,
				cancelText: '不保存',
				confirmText: '保存',
				success: (res) => {
					if (res.confirm) {
						store()
					} else {
						uni.removeStorage({
							key: 'add-input'
						})
					}
					uni.navigateBack({
						delta: 1
					})
				}
			})
			showBack.value = true
			return true
		}
	});
	// 上传图片
	const uploadImage = (event) => {
		instance.refs.imageBox.chooseFile()

	}
	// 删除图片
	const deletePic = (event) => {
		infoForm.imageList.splice(event.index, 1);
	};
	// 新增图片
	const afterRead = async (event) => {
		console.log(event);
		// 当设置 mutiple 为 true 时, file 为数组格式，否则为对象格式
		let lists = [].concat(event.file);
		let fileListLen = infoForm.imageList.length;
		lists.map((item) => {
			infoForm.imageList.push({
				...item,
				status: 'uploading',
				message: '上传中',
			});
		});
		const uploadFilePromise = (url) => {
			return new Promise((resolve, reject) => {
				let a = uni.uploadFile({
					url: 'http://192.168.2.21:7001/upload', // 仅为示例，非真实的接口地址
					filePath: url,
					name: 'file',
					formData: {
						user: 'test',
					},
					success: (res) => {
						setTimeout(() => {
							resolve(res.data.data);
						}, 1000);
					},
				});
			});
		};
	};
</script>
<style lang="scss">
	.add-input {
		margin: 0 10rpx;
	}

	.navbar-center {
		display: flex;
		flex-direction: row;
		align-items: center;
		height: 44rpx;
		line-height: 44rpx;
		justify-content: center;

		text {
			font-size: 32rpx;
		}
	}

	.footer {
		display: flex;
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		height: 80rpx;
		align-content: center;
		justify-content: space-between;

		.footer-left {
			display: flex;
			align-items: center;

			.footer-icon {
				margin-right: 20rpx;
			}
		}

		.footer-right {
			display: flex;
			align-items: center;
			margin-right: 20rpx;

			.submit {
				height: 60rpx;
			}

		}
	}
</style>