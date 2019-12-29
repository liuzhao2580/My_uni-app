<template>
	<view class="index">
		<!-- 滚动的导航栏 tab -->
		<swiperTab :tabBars="tabBars" :tabIndex="tabIndex" @tabber_tap="tabber_tap"/>
		<!-- 内容 -->
		<view class="uni-tab-bar">
			<swiper :current="tabIndex" class="swiper-box" :style="{height: swiper_Height + 'px'}" @change="swiper_change">
				<swiper-item v-for="(items,index) in newsList" :key="index">
					<scroll-view scroll-y class="list">
						<block v-for="(item,index1) in items.list" :key="index1">
							<indexList :item="item" :index="index1"/>
						</block>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import indexList from "../../../components/tabbar/index/index-list.vue"
	import swiperTab from "../../../components/common/swiper-tab.vue"
	export default {
		components: {
			indexList,
			swiperTab
		},
		data() {
			return {
				tabBars: [
					{
					    name: '关注',
					    id: 'guanzhu'
					}, 
					{
					    name: '推荐',
					    id: 'tuijian'
					}, 
					{
					    name: '体育',
					    id: 'tiyu'
					}, 
					{
					    name: '热点',
					    id: 'redian'
					}, 
					{
					    name: '财经',
					    id: 'caijing'
					},
					{
					    name: '动漫',
					    id: 'dongman'
					}
				],
				tabIndex: 0,
				swiper_Height: 500,
				/*
				is_focus // 是否关注过 true :关注  false: 未关注 
				type // 指出当前的文件类型
				evaluate_num // 设定评论  index 0 代表没有赞踩 1 代表赞 2 代表踩
				 */
				newsList: [
					{
						list : [
							{
								avtar_image: "/static/images/avtar-1.jpg",
								avtar_name: "小火车",
								is_focus: false,  // 是否关注过 true :关注  false: 未关注
								detele_title: "小火车况且况且",
								detele_image: "/static/images/detele-1.jpg",
								type: "image",
								evaluate_num: {
									index: 0,
									good_num: 20,
									bad_num: 2
								},
								new_num: 20,
								share_num: 10
							},
							{
								avtar_image: "/static/images/avtar.jpg",
								avtar_name: "小火车",
								is_focus: true,  // 是否关注过 true :关注  false: 未关注
								detele_title: "小火车况且况且",
								detele_image: "/static/images/detele-2.jpg",
								type: "video",
								play_num: "20W",
								play_long: "2:47",
								evaluate_num: {
									index: 1,
									good_num: 200,
									bad_num: 2
								},
								new_num: 20,
								share_num: 10
							}
						]
					},
					{
						list : [
							{
								avtar_image: "/static/images/avtar-1.jpg",
								avtar_name: "小松鼠",
								is_focus: false,  // 是否关注过 true :关注  false: 未关注
								detele_title: "小火车况且况且",
								detele_image: "/static/images/detele-1.jpg",
								type: "image",
								evaluate_num: {
									index: 0,
									good_num: 20,
									bad_num: 2
								},
								new_num: 20,
								share_num: 10
							}
						]
					},
					{},
					{},
					{},
					{}
				]
			}
		},
		onLoad() {
			uni.getSystemInfo({
			    success: (res) => {
					// 用来计算 当前屏幕的高度
					let height = res.windowHeight - uni.upx2px(100)
			        this.swiper_Height = height
			    }
			});
		},
		methods: {
			// 内容区域的滑动事件
			swiper_change(e) {
				let get_Index = e.detail.current
				this.tabIndex = get_Index
			},
			// 接收 swiperTab 组件点击的时候传递的参数
			tabber_tap(index) {
				this.tabIndex = index
			}
		}
	}
</script>

<style lang="scss">
	.index {
		padding-top: 20upx;
		
	}
</style>
