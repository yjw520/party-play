<template>
	<view>
		<u-transition :show="isNotFullScreen" mode="fade">
			<view class="custom-nav-bar" :style="{ top: barTop + 'px', height: barH + 'px' }">
				<view @click="goBack">
					<u-icon size="32" name="arrow-left" color="#fff"></u-icon>
				</view>
			</view>
		</u-transition>
		<view v-if="bgType == 'board'" class="light-wrap" :class="bgColor" @click="touchScreen"></view>
		<view v-else class="camera-wrap" @click="touchScreen">
			<camera class="camera" :class="bgColor" device-position="back" :flash="flash" binderror="error" :device-position="bgType" mode="normal">
				<view v-if="flashlight" class="camera-cover" :class="bgColor"></view>
				<view v-else class="camera-content" :class="bgColor"></view>
			</camera>
		</view>
		<u-transition :show="isNotFullScreen" mode="fade-down">
			<view class="footer-wrap">
				<view class="footer-item" @click="changesStyle">
					<u-badge numberType="overflow" :type="type" max="99" :value="curBgColorTypeIndex + 1" color="#fff" inverted="true" absolute="true" class="badge"></u-badge>
					<u-icon size="32" name="grid"></u-icon>
					<text>样式</text>
				</view>
				<view class="footer-item" @click="changeSpeed">
					<u-badge numberType="overflow" :type="type" max="99" :value="curSpeedIndex + 1" color="#fff" inverted="true" absolute="true" class="badge"></u-badge>
					<u-icon size="32" name="arrow-right-double"></u-icon>
					<text>速度</text>
				</view>
				<view class="footer-item" @click="toggleFlashlight">
					<u-icon size="32" name="info"></u-icon>
					<text>闪光灯</text>
				</view class="footer-item">
				<view class="footer-item" @click="toggleCamera">
					<u-icon size="32" name="camera"></u-icon>
					<text>相机</text>
				</view class="footer-item">
			</view>
		</u-transition>
		<u-toast ref="uToast"></u-toast>
	</view>
</template>

<script>
	const BOARD_TYPE = ['board', 'back', 'front'];
	const LIGHT_COLOR_TYPE = ['COLOR_TYPE1', 'COLOR_TYPE2', 'COLOR_TYPE3'];
	const LIGHT_COLOR_TYPE_MAP = {
		'COLOR_TYPE1': ['black', 'red'],
		'COLOR_TYPE2': ['red', 'blue', 'green'],
		'COLOR_TYPE3': ['blue','green']
	};
	const CHANGE_SPEED = [300, 250, 200, 100, 80 , 50];
	const CAMERA_TYPE = {
		board: '摄像已关闭',
		back: '后置摄像头已打开',
		front: '前置摄像头已打开'
	};
	

	export default {
		data() {
			return {
				barTop: 0,
				barH: 32,
				bgType: BOARD_TYPE[0],
				curBgTypeIndex: 0,
				isNotFullScreen: true,
				bgColorType: LIGHT_COLOR_TYPE[0],
				bgColor: '',
				curBgColorTypeIndex: 0,
				curBgColorIndex: 0,
				bgColorChangeSpeed: CHANGE_SPEED[0],
				timer: null,
				type: 'primary',
				curSpeedIndex: 0,
				flashlight: false,
				flash: 'off'
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
				this.isNotFullScreen = !this.isNotFullScreen;
			},
			changesStyle() {
				this.curBgColorTypeIndex = (this.curBgColorTypeIndex + 1) % LIGHT_COLOR_TYPE.length;
				this.bgColorType = LIGHT_COLOR_TYPE[this.curBgColorTypeIndex];
				this.curBgColorIndex = 0;
			},
			changeSpeed() {
				this.curSpeedIndex = (this.curSpeedIndex + 1) % CHANGE_SPEED.length;
				this.bgColorChangeSpeed = CHANGE_SPEED[this.curSpeedIndex];
				this.initLight();
			},
			toggleCamera() {
				if (this.flashlight) {
					this.flashlight = false;
				}

				this.curBgTypeIndex = (this.curBgTypeIndex + 1) % BOARD_TYPE.length;
				this.bgType = BOARD_TYPE[this.curBgTypeIndex];
				this.showToast({ duration: 500, message: CAMERA_TYPE[this.bgType] });
			},
			toggleFlashlight() {
				this.flashlight = !this.flashlight;

				const flash = this.flashlight ? 'torch' : 'off';
				const bgType = this.flashlight ? 'back' : 'board';

				this.bgType = bgType;
				this.flash = flash;
			},
			lightChange() {
				const lightColorType = LIGHT_COLOR_TYPE_MAP[this.bgColorType];

				this.curBgColorIndex = (this.curBgColorIndex + 1) % lightColorType.length;
				this.bgColor = lightColorType[this.curBgColorIndex];
			},
			initLight() {
				clearInterval(this.timer);
				this.timer = setInterval(() => {
					this.lightChange();
				}, this.bgColorChangeSpeed);
			},
			setScreenBrightness() {
				uni.setScreenBrightness({
					value: 1,
					success: function () {
					},
					fail: function () {
						console.error('屏幕亮度设置失败')
					}
				});

			},
			showToast(params) {
				this.$refs.uToast.show({
					...params
				})
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
			this.initLight();
			this.setScreenBrightness();
		},
		onUnload() {
			clearInterval(this.timer);
		}
	}
</script>

<style lang="scss">
	.custom-nav-bar {
		position: fixed;
		top: 40rpx;
		display: flex;
	    align-items: center;
	    justify-content: space-between;
	    height: 44px;
	    padding: 0 15px;
		color: #fff;
		z-index: 9999;
	}
	.light-wrap {
		background: #000;
		height: 100vh;
	}
	.camera {
		width: 100%;
		height: 100vh;
		.camera-content {
			height: 100%;
			opacity: .3;
		}
		.camera-cover {
			height: 100%;
		}
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
		.badge {
			z-index: 99;
		}
	}
	.red {
		background-color: red;
	}
	.blue {
		background-color: blue;
	}
	.green {
		background-color: green;
	}
	.black {
		background-color: #000;
	}
</style>