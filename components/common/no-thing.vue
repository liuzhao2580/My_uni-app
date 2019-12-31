<template>
	<view class="nothing-box">
		<image src="../../../static/images/nothing.png" mode="widthFix" class="image"></image>
	</view>
</template>

<script>
</script>

<style lang="scss" scoped>
	.nothing-box {
		display: flex;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: #FFFFFF;
		justify-content: center;
		.image {
			width: 50%;
		}
	}
</style>
