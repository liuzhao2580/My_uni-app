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
		<uploadImage></uploadImage>
		<!-- 弹出框 -->
		<uni-popup :show="showPopup">
			1111
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
				showPopup: true
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
	
</style>
