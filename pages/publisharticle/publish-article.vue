<template>
	<view>
		<!-- 标题导航栏 -->
		<uni-nav-bar 
		left-icon="arrowleft"
		:statusBar="true"
		@clickLeft="back" 
		rightText="发布" 
		@clickRight="publish">
		<view class="nav-bar-title" @tap="allORself">
			<text>{{allORself_title}}</text>
			<text class="iconfont icon-arrow-left1"></text>
		</view>
		</uni-nav-bar>
		<!-- 内容文本输入框 -->
		<view class="textarea-box uni-textarea">
			<textarea v-model="textarea_value" placeholder="" />
		</view>
		<!-- 上传图片 -->
		<view class="uni-list list-pd">
			<view class="uni-list-cell cell-pd">
				<view class="uni-uploader">
					<view class="uni-uploader-head">
						<view class="uni-uploader-title">点击可预览选好的图片</view>
						<view class="uni-uploader-info">{{imageList.length}}/9</view>
					</view>
					<view class="uni-uploader-body">
						<view class="uni-uploader__files">
							<block v-for="(image,index) in imageList" :key="index">
								<view class="uni-uploader__file image-box">
									<text class="iconfont icon-error delete-image" @tap="delete_image(index)"></text>
									<image class="uni-uploader__img" :src="image" :data-src="image" @tap="previewImage"></image>
								</view>
							</block>
							<view class="uni-uploader__input-box">
								<view class="uni-uploader__input" @tap="chooseImage"></view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from "../../components/common/uni-nav-bar/uni-nav-bar.vue"
	var sourceType = [
		['camera'],
		['album'],
		['camera', 'album']
	]
	var sizeType = [
		['compressed'],
		['original'],
		['compressed', 'original']
	]
	export default {
		components: {
			UniNavBar
		},
		data() {
			return {
				allORself_title: "所有人可见",
				textarea_value: "",
				imageList: [],
				sourceTypeIndex: 2,
				sourceType: ['拍照', '相册', '拍照或相册'],
				sizeTypeIndex: 2,
				sizeType: ['压缩', '原图', '压缩或原图'],
				countIndex: 8,
				count: [1, 2, 3, 4, 5, 6, 7, 8, 9]
			};
		},
		methods: {
			// 点击返回事件
			back() {
				uni.navigateBack({
					delta:1
				})
			},
			// 发布的点击事件
			publish() {
				console.log(222)
			},
			// 设置 所有人和仅自己可见
			allORself() {
				const itemTitle = ["所有人可见","仅自己可见"]
				uni.showActionSheet({
				    itemList : itemTitle,
				    success: (res) => {
				        this.allORself_title = itemTitle[res.tapIndex]
				    }
				});
			},
			// 删除选中的图片
			delete_image(index) {
				this.imageList.splice(index, 1)
			},
			chooseImage: async function() {
				// #ifdef APP-PLUS
				// TODO 选择相机或相册时 需要弹出actionsheet，目前无法获得是相机还是相册，在失败回调中处理
				if (this.sourceTypeIndex !== 2) {
					let status = await this.checkPermission();
					if (status !== 1) {
						return;
					}
				}
				// #endif
			
				if (this.imageList.length === 9) {
					let isContinue = await this.isFullImg();
					console.log("是否继续?", isContinue);
					if (!isContinue) {
						return;
					}
				}
				uni.chooseImage({
					sourceType: sourceType[this.sourceTypeIndex],
					sizeType: sizeType[this.sizeTypeIndex],
					count: this.imageList.length + this.count[this.countIndex] > 9 ? 9 - this.imageList.length : this.count[this.countIndex],
					success: (res) => {
						this.imageList = this.imageList.concat(res.tempFilePaths);
					},
					fail: (err) => {
						// #ifdef APP-PLUS
						if (err['code'] && err.code !== 0 && this.sourceTypeIndex === 2) {
							this.checkPermission(err.code);
						}
						// #endif
						// #ifdef MP
						uni.getSetting({
							success: (res) => {
								let authStatus = false;
								switch (this.sourceTypeIndex) {
									case 0:
										authStatus = res.authSetting['scope.camera'];
										break;
									case 1:
										authStatus = res.authSetting['scope.album'];
										break;
									case 2:
										authStatus = res.authSetting['scope.album'] && res.authSetting['scope.camera'];
										break;
									default:
										break;
								}
								if (!authStatus) {
									uni.showModal({
										title: '授权失败',
										content: 'Hello uni-app需要从您的相机或相册获取图片，请在设置界面打开相关权限',
										success: (res) => {
											if (res.confirm) {
												uni.openSetting()
											}
										}
									})
								}
							}
						})
						// #endif
					}
				})
			},
			isFullImg: function() {
				return new Promise((res) => {
					uni.showModal({
						content: "已经有9张图片了,是否清空现有图片？",
						success: (e) => {
							if (e.confirm) {
								this.imageList = [];
								res(true);
							} else {
								res(false)
							}
						},
						fail: () => {
							res(false)
						}
					})
				})
			},
			previewImage: function(e) {
				var current = e.target.dataset.src
				uni.previewImage({
					current: current,
					urls: this.imageList
				})
			},
			async checkPermission(code) {
				let type = code ? code - 1 : this.sourceTypeIndex;
				let status = permision.isIOS ? await permision.requestIOS(sourceType[type][0]) :
					await permision.requestAndroid(type === 0 ? 'android.permission.CAMERA' :
						'android.permission.READ_EXTERNAL_STORAGE');
			
				if (status === null || status === 1) {
					status = 1;
				} else {
					uni.showModal({
						content: "没有开启权限",
						confirmText: "设置",
						success: function(res) {
							if (res.confirm) {
								permision.gotoAppSetting();
							}
						}
					})
				}
			
				return status;
			}
		}
	}
</script>

<style lang="scss">
	.nav-bar-title {
		margin: auto;
	}
	.textarea-box {
		/deep/ .uni-textarea-wrapper {
			border: 1px solid #EEEEEE;
			border-radius: 10upx;
		}
	}
	.image-box {
		position: relative;
		.delete-image {
			z-index: 10;
			position: absolute;
			right: 0;
			top: -5upx;
		}
	}
</style>
