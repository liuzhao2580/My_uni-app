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
		<uploadImage @upload_image="uploadImage"></uploadImage>
		<!-- 弹出框 -->
		<uni-popup ref="showpopup">
			<view class="popup-box">
				<image src="../../static/images/publish-img.png" mode="widthFix" class="popup-image"></image>
				<view class="popup-text">
					<view>1.不可发布违法消息</view>
					<view>2.不可发布违法消息</view>
					<view>3.不可发布违法消息</view>
					<view>4.不可发布违法消息</view>
					<view>5.不可发布违法消息</view>
				</view>
				<button type="primary" class="popup-btn" @tap="popupClose">知道了</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import UniNavBar from "../../components/common/uni-nav-bar/uni-nav-bar.vue"
	import uploadImage from "../../components/common/upload-image.vue"
	import uniPopup from "../../components/common/uni-popup/uni-popup.vue"
	export default {
		components: {
			UniNavBar,
			uploadImage,
			uniPopup
		},
		data() {
			return {
				allORself_title: "所有人可见",
				textarea_value: "",
				showPopup: true,
				imageList: [],
				is_save: false,  // 是否保存为草稿
			};
		},
		onLoad() {
			this.$nextTick(() => {
				this.$refs["showpopup"].open()
			})
		},
		// 监听页面返回
		onBackPress(e) {
			if(!this.textarea_value && this.imageList.length < 1) return
			if(this.is_save) {
				return
			}
			else {
				uni.showModal({
					content: "是否保存为草稿",
					cancelText: "不保存",
					confirmText: "保存",
					success:(res) => {
						// 用户点击保存
						if(res.confirm) {
							console.log("保存")
						}
						// 用户点击不保存
						else if(res.cancel){
							console.log("不保存")
						}
						this.is_save = true
						uni.navigateBack({
							delta:1
						})
					}
				})
				return true
			}
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
				this.$nextTick(() => {
					this.$refs["showpopup"].open()
				})
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
			// 弹框关闭
			popupClose() {
				this.$nextTick(() => {
					this.$refs["showpopup"].close()
				})
			},
			// 接收多图上传 组件的参数
			uploadImage(upload_imageList) {
				this.imageList = upload_imageList
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
	.popup-box {
		display: flex;
		flex-direction: column;
		background-color: #fff;
		border-radius: 10upx;
		width: 500upx;
		.popup-image {
			border-radius: 10upx;
			width: 100%;
		}
		.popup-text {
			padding: 20upx;
			> view {
				margin: 10upx 0;
				font-size: 24upx;
			}
		}
		.popup-btn {
			width: 90%;
			margin-bottom: 20upx;
			background-color: #ffe934;
			color: #000;
			font-size: 30upx;
		}
	}
</style>
