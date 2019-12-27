<template>
	<view class="index">
		<view class="detele-box">
			<view>
				<!-- 头部 -->
				<view class="detele-header uni-flex">
					<!-- 头像 -->
					<view class="avtar">
						<image src="/static/images/avtar.jpg" mode="scaleToFill"></image>
						<text>小火车</text>
					</view>
					<!-- 关注 和 关闭 -->
					<view class="focus-box">
						<text class="focus">
							<text class="iconfont icon-jia"></text>
							<text>关注</text>
						</text>
						<!-- 关闭 -->
						<text class="iconfont icon-error"></text>
					</view>
				</view>
				<!-- 内容 -->
				<view class="detele-content">
					<view>小火车况且况且</view>
					<image src="/static/images/detele-2.jpg" mode="scaleToFill"></image>
					<view class="play-box iconfont icon-bofang"></view>
					<view class="play-detele">
						<text class="iconfont icon-yanjing"></text>
						<text>20W&nbsp;次播放&nbsp;2:47</text>
					</view>
				</view>
				<!-- 底部 -->
				<view class="detele-bottom uni-flex">
					<!-- 评价 -->
					<view class="bottom-evaluate">
						<text class="iconfont icon-weixiao">
							<text>10</text>
						</text>
						<text class="iconfont icon-ku">
							<text>10</text>
						</text>
					</view>
					<!-- 分享 -->
					<view class="bottom-share">
						<text class="iconfont icon-xiaoxi">
							<text>10</text>
						</text>
						<text class="iconfont icon-fenxiang">
							<text>10</text>
						</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				index_detele: [
					{
						avtar_image: "/static/images/avtar.jpg",
						avtar_name: "小火车",
						is_focus: false,  // 是否关注过 true :关注  false: 未关注
						detele_title: "小火车况且况且",
						detele_image: "/static/images/detele-2.jpg",
						play_num: "20W",
						play_long: "2:47"
					}
				]
			}
		},
	}
</script>

<style lang="scss">
	.index {
		padding-top: 20upx;
		.detele-box {
			border-bottom: 1px solid #d4d4d4;
			>view {
				padding: 0 20upx;
			}
			// 头部
			.detele-header {
				justify-content: space-between;
				align-items: center;
				margin-bottom: 20upx;
				.avtar {
					image {
						width: 80upx;
						height: 80upx;
						border-radius: 40%;
						vertical-align: middle;
						margin-right: 10upx;
					}
					text {
						color: #c4c4c4;
					}
				}
				.focus-box {
					.focus {
						padding: 4upx 8upx;
						background-color: #f4f4f4;
						margin-right: 20upx;
						color: #2c2c2c;
						.iconfont {
							color: #2c2c2c;
							margin-right: 10upx;
						}
					}
						
					.iconfont {
						font-size: 18upx;
						color: #c4c4c4;
					}
				}
			}
			// 内容
			.detele-content {
				position: relative;
				height: 460upx;
				view {
					height: 60upx;
				}
				image {
					width: 100%;
					height: 400upx;
					border-radius: 20upx;
				}
				.play-box, {
					position: absolute;
					left: 50%;
					top: 50%;
					transform: translate(-50%, -50%);
					color: #FFFFFF;
					font-size: 60upx;
				}
				.play-detele {
					position: absolute;
					color: #FFFFFF;
					right: 10upx;
					bottom: 10upx;
					background-color: #1e1e1e;
					padding: 0 20upx;
					border-radius: 40upx;
					height: 60upx;
					line-height: 60upx;
					font-size: 22upx;
					opacity: 0.8;
					.iconfont {
						font-size: 22upx;
						margin-right: 10upx;
					}
				}
			}
			// 底部
			.detele-bottom {
				justify-content: space-between;
				color: #d4d4d4;
				.iconfont {
					height: 120upx;
					line-height: 120upx;
					display: inline-block;
					text {
						margin: 0 15upx;
					}
				}
			}
		}
	}
</style>
