<template>
	
	<view class="light-wrap" @click="touchScreen">
		<view class="custom-nav-bar" :style="{ top: barTop + 'px', height: barH + 'px' }">
			<view @click="goBack">
				<u-icon size="32" name="arrow-left" color="#fff"></u-icon>
			</view>
		</view>
		
		<view v-if="bgType !== 'board'">
			<camera class="camera" device-position="back" flash="off" binderror="error" :device-position="bgType"	mode="normal"></camera>
		</view>

		<view class="footer-wrap">
			<view class="footer-item" @click="changesStyle">
				<u-icon size="32" name="grid"></u-icon>
				<text>样式</text>
			</view>
			<view class="footer-item" @click="changeSpeed">
				<u-icon size="32" name="arrow-right-double"></u-icon>
				<text>速度</text>
			</view>
			<view class="footer-item" @click="toggleCamera">
				<u-icon size="32" name="camera"></u-icon>
				<text>相机</text>
			</view class="footer-item">
		</view>
	</view>
</template>

<script>
	const BOARD_TYPE = ['borad', 'front', 'back']

	export default {
		data() {
			return {
				barTop: 0,
				barH: 32,
				// bgType: BOARD_TYPE.BOARD,
				// devicePosition: 'front',
				curBgTypeIndex: 0,
			}
		},
		computed: {
			bgType() {
				return BOARD_TYPE[this.curBgTypeIndex];
			}
		},
		methods: {
			getBarHeihgt(sysInfo) {
				const capH = uni.getMenuButtonBoundingClientRect();
			
				this.barTop = capH.top;
				this.barH = capH.height;
			},
			goBack() {
				uni.navigateBack();
			},
			touchScreen() {
				console.log(666);
			},
			changesStyle() {
				
			},
			changeSpeed() {},
			toggleCamera() {
				this.curBgTypeIndex = (this.curBgTypeIndex + 1) % BOARD_TYPE.length;
				console.log(this.bgType);
			}
		},
		onLoad() {
			const that = this;
			uni.getSystemInfo({
				success: async function(res) {
					that.getBarHeihgt(res);
				},
				fail: function(err){
					console.error(err);
				}
			});
		},
	}
</script>

<style lang="scss">
	.light-wrap {
		background: #000;
		height: 100vh;
		.custom-nav-bar {
			position: fixed;
			top: 40rpx;
			display: flex;
		    align-items: center;
		    justify-content: space-between;
		    height: 44px;
		    padding: 0 15px;
			color: #fff;
			z-index: 999;
		}
		.camera {
			width: 100%;
			height: 100vh;;
		}
		.footer-wrap {
			display: flex;
			justify-content: space-between;
			color: #fff;
			position: fixed;
			bottom: 0px;
			width: 100%;
			.footer-item {
				display: flex;
				flex-direction: column;
				flex: 1;
				padding: 36rpx 0rpx;
				font-size: 28rpx;
				align-items: center;
			}
			
		}
	}
</style>