<template>
	<view class="detele-box">
		<view>
			<!-- 头部 -->
			<view class="detele-header uni-flex">
				<!-- 头像 -->
				<view class="avtar">
					<image :src="item.avtar_image" mode="scaleToFill"></image>
					<text>{{item.avtar_name}}</text>
				</view>
				<!-- 关注 和 关闭 -->
				<view class="focus-box">
					<text class="focus" v-if="!item.is_focus">
						<text class="iconfont icon-jia"></text>
						<text>关注</text>
					</text>
					<!-- 关闭 -->
					<text class="iconfont icon-error"></text>
				</view>
			</view>
			<!-- 内容 -->
			<view class="detele-content">
				<view>{{item.detele_title}}</view>
				<image :src="item.detele_image" mode="scaleToFill"></image>
				<template v-if="item.type == 'video'">
					<view class="play-box iconfont icon-bofang"></view>
					<view class="play-detele">
						<text class="iconfont icon-yanjing"></text>
						<text>{{item.play_num}}&nbsp;次播放&nbsp;{{item.play_long}}</text>
					</view>
				</template>
			</view>
			<!-- 底部 -->
			<view class="detele-bottom uni-flex">
				<!-- 评价 -->
				<view class="bottom-evaluate">
					<text :class="[{'active': item.evaluate_num.index == 1},'iconfont icon-weixiao']">
						<text>{{item.evaluate_num.good_num}}</text>
					</text>
					<text :class="[{'active': item.evaluate_num.index == 2},'iconfont icon-ku']">
						<text>{{item.evaluate_num.bad_num}}</text>
					</text>
				</view>
				<!-- 分享 -->
				<view class="bottom-share">
					<text class="iconfont icon-xiaoxi">
						<text>{{item.new_num}}</text>
					</text>
					<text class="iconfont icon-fenxiang">
						<text>{{item.share_num}}</text>
					</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "index-list",
		props: {
			item: {
				default: () => {}
			},
			index: {
				default: Number
			}
		}
	}
</script>

<style lang="scss" scoped>
	.detele-box {
		border-bottom: 1px solid #d4d4d4;
		&:last-of-type {
			border-bottom: 0;
		}
		>view {
			padding: 20upx 20upx 0;
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
			.bottom-evaluate {
				.active {
					color: #f0e798;
				}
			}
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
</style>
