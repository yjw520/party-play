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
				wx.startDeviceMotionListening({
				  interval: 'normal',
				  success: function () {
					wx.onDeviceMotionChange(function (res) {
						console.log('=========>6');
						console.log(res);
					  var beta = res.beta; // 获取设备在 beta 
					  const gamma = res.gamma;
					  if (gamma > -50) {
						console.log('=====>up');
					  } else if (gamma < -80) {
						console.log('=====>down');
					  }
					});
				  }
				});
			},
			stop(){
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