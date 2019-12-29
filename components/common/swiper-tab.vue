<template>
	<view class="uni-tab-bar">
		<scroll-view class="uni-swiper-tab" scroll-x :show-scrollbar="false">
			<view v-for="(tab,index) in tabBars" :key="tab.id" class="swiper-tab-list" @tap="tabber_tap(index)">
				<view class="uni-tab-item-title" :class=" tabIndex == index ? 'active' : ''">{{tab.name}}</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props: {
			// 接收导航栏需要的数组
			tabBars: Array,
			// 接收导航栏的当前的索引
			tabIndex: Number
		},
		methods: {
			// 导航栏的点击事件
			tabber_tap(index) {
				this.$emit("tabber_tap", index)
			}
		}
	}
</script>

<style lang="scss" scoped>
	// 导航栏
	.uni-tab-bar {
		.uni-tab-item-title {
			color: #989898;
			&.active {
				color: #3a3a3a;
				position: relative;
				&:after {
					position: absolute;
					bottom: 0;
					left: 50%;
					transform: translateX(-50%);
					content: "";
					width: 80upx;
					height: 10upx;
					background-color: #fede33;
					border-radius: 10upx;
				}
			}
		}
	}
</style>
