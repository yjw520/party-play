<template>
	<view>
		<u-transition :show="isNotFullScreen" mode="fade">
			<view class="custom-nav-bar" :style="{ top: barTop + 'px', height: barH + 'px' }">
				<view @click="goBack">
					<u-icon size="32" name="arrow-left" color="#fff"></u-icon>
				</view>
			</view>
		</u-transition>
		
		<view class="barrage-wrap" @click="touchScreen">
			<view class="barrage-text-wrap">
				<text class="barrage-text" :animation="animationData"
					:style="{ right: barrageRight + 'px', color: barrageColor, fontSize: fontSize + 'rpx',  }"
				>{{ displayText }}</text>
			</view>
		</view>
		<u-popup :show="patternShow" @close="close" bgColor="rgba(65, 65, 65, 0.5)">
			<view class="pop-wrap">
				<text> (゜-゜)つ点击非选项区域就可以返回哦！</text>
				<view v-if="op == 'pattern'" class="barrage-pattern">
					<text>普通模式</text>
					<u-switch v-model="pattern" size="28" @change="changePattern"></u-switch>
					<text>旋转模式</text>
				</view>
				<view class="barrage-poptext" v-if="op === 'text'">
					<view>
						<u--input
							placeholder="请输入文字"
							border="surround"
							shape="circle"
							color="#fff"
							v-model="text"
						>
						</u--input>
					</view>
					<view class="pop-button">
						<u-button type="primary" text="发送" shape="circle" @click="changeText"></u-button>
					</view>
				</view>
				<view class="barrage-font" v-if="op === 'font'">
					<view>
						<text class="barrage-size">大小</text>
						<u-slider v-model="slider" min="50" @change="changeSize"></u-slider>
					</view>
					<view>
						<text class="color-text">推荐颜色</text>
						<view  class="barrage-font-color">
							<u-tag v-for="(item, index) in tagArray" :key="index" :bgColor="item" @click="changeColor(item)" />
						</view>
					</view>
				</view>
				<view class="barrage-font" v-if="op === 'speed'">
					<text class="barrage-size">速度</text>
					<u-slider v-model="speed" min="1" max="5" @change="changeSpeed"></u-slider>
				</view>
			</view>
		</u-popup>
		<u-transition :show="isNotFullScreen" mode="fade">
			<view class="footer-wrap">
				<view class="footer-item" @click="open({ active: 'text' })">
					<u-icon size="32" name="list-dot"></u-icon>
					<text>文字</text>
				</view>
				<view class="footer-item" @click="open({ active: 'pattern' })">
					<u-icon size="32" name="thumb-up"></u-icon>
					<text>模式</text>
				</view>
				<view class="footer-item" @click="open({ active: 'font' })">
					<u-icon size="32" name="grid-fill"></u-icon>
					<text>颜色</text>
				</view>
				<view class="footer-item" @click="open({ active: 'speed' })">
					<u-icon size="32" name="arrow-right-double"></u-icon>
					<text>速度</text>
				</view class="footer-item">
			</view>
		</u-transition>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				displayText: '手持弹幕',
				text: '',
				animationData: {},
				curSpeed: 6000,
				speed: 1,
				wH: 753,
				barrageLen: 0,
				initTimer: null,
				timer: null,
				barrageRight: -400,
				barrageColor: '#fff',
				patternShow: false,
				pattern: false,
				op: '',
				tagArray: ['#FF0000', '#FF5733', '#FFFF00', '#00FF00', '#fff', '#0000FF', '#7F3C8D'],
				slider: 50,
				fontSize: 250,
				barTop: 0,
				barH: 32,
				isNotFullScreen: true
			};
		},
		methods: {
			/**
			 * 改变文字
			 */
			changeText() {
				this.displayText = this.text;
				this.clearAnimation();
				this.rollAnimation();
			},
			/**
			 * 改变模式
			 */
			changePattern(value) {
				this.clearAnimation();
				this.rollAnimation();
			},
			/**
			 * 改变颜色
			 */
			changeColor(color) {
				this.barrageColor = color;
			},
			/**
			 * 改变大小
			 */
			changeSize(value) {
				this.fontSize = value * 5;
				this.clearAnimation();
				this.rollAnimation();
			},
			/**
			 * 改变速度
			 */
			changeSpeed(value) {
				const speed = {
					1: 6000,
					2: 5000,
					3: 4000,
					4: 3000,
					5: 2000,
				};
				this.curSpeed = speed[`${value}`];
				this.clearAnimation();
				this.rollAnimation();
			},
			clearAnimation () {
				if (this.initTimer) {
					clearTimeout(this.initTimer);
				}
				clearInterval(this.timer);
				this.initRollAnimation();
			},
			/**
			 * 获取字幕长度
			 */
			getBarrageLen() {
				return new Promise((resolve, reject) => {
					this.$nextTick(() => {
						const query = uni.createSelectorQuery().in(this);
						query.select('.barrage-text').boundingClientRect(data => {
							const { height } = data;
							
							this.barrageLen = height;
							this.barrageRight = -this.barrageLen;
							resolve();
						}).exec();
					})
				});
			},
			/**
			  * 动画
			  */
			async rollAnimation() {
				const res = await this.getBarrageLen();
				const startP = this.wH + this.barrageLen;
				const duration = this.curSpeed;
				const barrageAnimation = function() {
					if (this.pattern) {
						this.animation.translateX(`-${startP}px`).rotate(360).step({
							duration,
						});
					} else {
						this.animation.translateX(`-${startP}px`).step({
							duration,
						});
					}
					
					this.animationData = this.animation.export();
					
					this.initTimer = setTimeout(() => {
						this.initRollAnimation();
					}, duration);
				}.bind(this);
				
				barrageAnimation();

				this.timer = setInterval(() => {
					barrageAnimation();
				}, duration + 100);
			},
			getBarHeihgt(sysInfo) {
				const capH = uni.getMenuButtonBoundingClientRect();
				const navH = (capH.top - sysInfo.statusBarHeight) * 2 + capH.height;

				this.barTop = capH.top;
				this.barH = capH.height;
				return capH;
			},
			initRollAnimation() {
				if (this.pattern) {
					this.animation.translateX(0).rotate(0).step({
						duration: 0,
					});
				} else {
					this.animation.translateX(0).step({
						duration: 0,
					});
				}
				this.animationData = this.animation.export();
			},
			goBack() {
				uni.navigateBack();
			},
			open(data) {
			  const { active } = data;

			  this.op = active;
			  this.patternShow = true;
			},
			close() {
			  this.patternShow = false;
			  if (this.op === 'text') {
				  this.text = '';
			  }
			},
			touchScreen() {
				this.isNotFullScreen = !this.isNotFullScreen;
				console.log(66);
			},
		},
		onLoad() {
			const that = this;
			uni.getSystemInfo({
				success: async function(res) {
					const { windowHeight } = res;

					that.wH = windowHeight;
					await that.getBarrageLen();
					that.getBarHeihgt(res);
				},
				fail: function(err){
					console.error(err);
				}
			});
		},
		onShow() {
			const animation = uni.createAnimation({
				// duration:60000,
				timingFunction: 'linear',
			});
			this.animation = animation;
			this.rollAnimation();
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
		z-index: 999;
	}
	.barrage-wrap {
		color: #fff;
		.barrage-text-wrap {
			width: 100vh;
			height: 100.2vw;
			background-color: #000;
			overflow: hidden;
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%) rotate(90deg);
			line-height: 1;
			.barrage-text {
				// padding-left: 100vh;
				// position: absolute;
				// top: 50%;
				// left: 0;
				white-space: nowrap;
				// margin-top: -.5em;
				position: absolute;
				// left: 0;
				// top: 50%;
				// transform: translateY(-50%);
				line-height: 100vw;
				font-size: 80px;
				right: -400px;
			}
		}
	}
	.pop-wrap {
		color: #fff;
		padding: 20rpx;
		.barrage-pattern {
			display: flex;
			justify-content: space-around;
			align-items: center;
			padding: 20rpx 66rpx 10rpx;
		}
		.barrage-poptext {
			display: flex;
			align-items: center;
			padding: 20rpx 66rpx 10rpx;
			.pop-button {
				width: 120rpx;
				margin-left: 20rpx;
			}
		}
		.barrage-font {
			display: flex;
			padding: 20rpx 66rpx 10rpx;
			flex-direction: column;
			.barrage-font-color {
				display: flex;
				justify-content: space-around;
				margin-top: 20rpx;
			}
			.barrage-size {
				margin-left: 20rpx;
			}
			.color-text {
				margin-left: 20rpx;
			}
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
		
	}
</style>