<template>
	<view class="dynamic-box">
		<!-- 标题导航栏 -->
		<uni-nav-bar 
		:statusBar="true"
		@clickLeft="checkIn"
		@clickRight="publish"
		class="uni-bar-box">
			<!-- 左边 -->
			<view class="navbar-left" slot="left">
				<view class="iconfont icon-qiandao"></view>
			</view>
			<!-- 中间 -->
			<view class="navbar-center">
				<template v-for="(item,index) in navbarList">
					<view :class="[{'active': navbarIndex == index},'select']" :key="item.id" @tap="selectChange(index)">
						{{item.name}}
					</view>
				</template>
			</view>
			<!-- 右边 -->
			<view class="navber-right" slot="right">
				<view class="iconfont icon-bi"></view>
			</view>
		</uni-nav-bar>
	</view>
</template>

<script>
	import UniNavBar from "../../../components/common/uni-nav-bar/uni-nav-bar.vue"
	export default {
		components:{
			UniNavBar
		},
		data() {
			return {
				navbarIndex: 0,
				navbarList: [
					{
						name: "关注",
						id: "focus"
					},
					{
						name: "话题",
						id: "topic"
					}
				]
			};
		},
		methods: {
			// 签到
			checkIn() {
				
			},
			// 发布按钮
			publish() {
				uni.navigateTo({
					url: "../../publisharticle/publish-article"
				})
			},
			// 导航栏的点击事件
			selectChange(index) {
				this.navbarIndex = index
			}
		}
	}
</script>

<style lang="scss">
.dynamic-box {
	.uni-bar-box {
		.navbar-left {
			.iconfont {
				color: #ffe934;
			}
		}
		.navbar-center {
			display: flex;
			margin: 0 auto;
			.select {
				color: #969696;
				padding: 0 20upx;
				&.active {
					color: #343434;
					position: relative;
					&::after {
						content: "";
						width: 70%;
						height: 8upx;
						border-radius: 5upx;
						background-color: #ffe934;
						position: absolute;
						bottom: 0;
						left: 50%;
						transform: translateX(-50%);
					}
				}
			}
		}
		/deep/ .uni-navbar__header{  
			.uni-navbar__header-btns {
				&:last-of-type {
					justify-content: flex-end;
				}
			}
		}
		.navber-right {
		}
		.iconfont {
			font-size: 36upx;
		}
	}
}
</style>
