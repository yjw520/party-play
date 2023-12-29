<template>
	<view class="pro-wrap">
		<view class="wrap-text" v-if="count === 0">
			{{ text }}
		</view>
		<view class="wrap-text" v-else>
			{{ count }}
		</view>
		<button @click="start">开始监听陀螺仪变化</button>
		<button @click="stop">停止监听陀螺仪变化</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				timer: null,
				count: 3,
				text: 'hah',
				textArr: ['哈哈', '哈哈','哈哈','哈哈','哈哈','哈哈','哈哈','哈哈','哈哈','哈哈','哈哈','哈哈','哈哈','哈哈','哈哈','哈哈'],
			};
		},
		methods: {
			start() {
				// uni.onGyroscopeChange((res) => {
				// 	console.log('gyroData.rotationRate.x = ' + res.x)
				// 	console.log('gyroData.rotationRate.y = ' + res.y)
				// 	console.log('gyroData.rotationRate.z = ' + res.z)
				// 	console.log(res);
				// 	const { x, y, z } = res;
				// 	if ((x > -1 && x < 1) && (y > -1 && y < 1) && (z > 8 && z < 10)) {
				// 	    // 手机处于屏幕朝下的状态
				// 	    console.log("手机处于屏幕朝下的状态");
				// 	    // 可以在这里根据手机的朝向执行相应的操作
				// 	  }
				// });
				// uni.startGyroscope({
				// 	interval: "normal",
				// 	success() {
				// 		console.log('success')
				// 	},
				// 	fail() {
				// 		console.log('fail')
				// 	}
				// })
				wx.startDeviceMotionListening({
				  success: function () {
					wx.onDeviceMotionChange(function (res) {
						console.log('=========>6');
						console.log(res);
					  var beta = res.beta; // 获取设备在 beta 轴的旋转角度
					  if (beta > 90 || beta < -90) {
						console.log('=====>up');
					  } else {
						console.log('=====>down');
					  }
					});
				  }
				});
				// uni.onCompassChange((res) => {
				// 	console.log('==========>');
				// 	console.log(res);
				// });
				// uni.startCompass();
			},
			stop(){
				// uni.offCompassChange(() => {
				// 	console.log('==========>');
				// 	console.log(res);
				// });
				// uni.stopGyroscope({
				// 	success() {
				// 		console.log('stop success!')
				// 	},
				// 	fail() {
				// 		console.log('stop fail!')
				// 	}
				// })
				// uni.stopCompass();
				wx.stopDeviceMotionListening();
			}
		},
		onLoad(option) {
			console.log(option);
			this.timer = setInterval(() => {
				this.count -= 1;
				if (this.count === 0) {
					clearInterval(this.timer);
				}
			}, 1000);
		},
	}
</script>

<style lang="scss">
	.pro-wrap {
		width: 100%;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		.wrap-text {
			// transform: rotate(90deg);
			 writing-mode: vertical-rl; /* 设置文字纵向排列 */
			 font-size: 100px;
			 font-weight: bolder;
		}
	}
</style>