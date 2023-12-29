<template>
	<view class="home-wrap">
		<view class="night-wrap">
			<view class="night">
				<view class="shooting-star"></view>
				<view class="shooting-star"></view>
				<view class="shooting-star"></view>
				<view class="shooting-star"></view>
				<view class="shooting-star"></view>
				<view class="shooting-star"></view>
				<view class="shooting-star"></view>
				<view class="shooting-star"></view>
				<!-- <view class="shooting-star"></view>
				<view class="shooting-star"></view>
				<view class="shooting-star"></view>
				<view class="shooting-star"></view> -->
			</view>
		</view>
		<div class="bulb-container">
			<button class="bulb">
			  <div class="bulb__image">
				<img src="//www.w3cplus.com/sites/default/files/blogs/2020/2002/bulb-on.png" alt="Swining Light Bulb" />
			  </div>
			</button>
		</div>
		<view class="notice-bar">
			<u-notice-bar text="什么你在吃香菜"></u-notice-bar>
		</view>
		<view class="card-wrap">
			<u-transition :show="show" mode="slide-left">
			<view class="guess-card" @click="goGuessCate">
				<image class="guess-img" src="../../static/image/paint.png" mode=""></image>
				<text>你画我猜</text>
			</view>
			</u-transition>
			<u-transition :show="show" mode="slide-right">
			<view class="hand-wrap">
				<view class="barrage-card" @click="goBarrage">
					<text>手持弹幕</text>
				</view>
				<view class="lamp-card" @click="goBarrage2">
					<text class="lamp-text">夜店手灯</text>
					<image class="lamp-img" src="../../static/image/lamp.png" mode=""></image>
				</view>
			</view>
			</u-transition>
		</view>
	</view>
</template>

<script>
	 export default {
	        data() {
	            return {
	                show: true
	            }
	        },
			methods: {
				goGuessCate() {
					uni.navigateTo({
						url: '/pages/guess-category/index',
					});
				},
				goBarrage() {
					uni.navigateTo({
						url: '/pages/barrage/index',
					});
				},
				goBarrage2() {
					uni.navigateTo({
						url: '/pages/test/index',
					})
				}
			},
			onShow() {
				console.log(666);
				this.show = true;
			},
			onHide() {
				console.log('222');
				this.show = false;
			}
	    }
</script>

<style lang="scss">
	.home-wrap {
		background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
		height: 100vh;
		overflow: hidden;
		.card-wrap {
			display: flex;
			height: 180px;
			padding: 20px 30px;
			justify-content: space-between;
			.guess-card {
				width: 130px;
				height: 100%;
				color: #fff;
				background-image: linear-gradient(274deg, #c05e4b, #b46870, #a27295, #867cbb);
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: space-around;
				border-radius: 10px;
				.guess-img {
					width: 78px;
					height: 77px;
				}
			}
			.hand-wrap {
				display: flex;
				flex-direction: column;
				width: 180px;
				height: 100%;
				justify-content: space-between;
				.barrage-card {
					color: #fff;
					height: 50px;
					background-image: linear-gradient(25deg, #d2443e, #e37469, #f1a097, #f9cbc7);
					border-radius: 10px;
					display: flex;
					justify-content: center;
					align-items: center;
				}
				.lamp-card {
					color: #fff;
					height: 118px;
					border-radius: 10px;
					background-image: url('../../static/image/bg-lamp.png');
					display: flex;
					.lamp-text {
						margin-top: 20px;
						margin-left: 22px;
					}
					.lamp-img {
						width: 69px;
						height: 69px;
						align-self: center;
					}
				}
			}
		}
	}
	.night-wrap {
		// width: 100vw;
		// height: 100vh;
		position: absolute;
	}
.night {
  width: 300rpx;
  height: 600rpx;
  // height: 100%;
  // width: 100vw;
  // height: 100vh;
  transform: rotateZ(45deg);
}

.shooting-star {
  position: absolute;
  left: 50%;
  top: 50%;
  height: 2px;
  background: linear-gradient(-45deg, #5f91ff, rgba(0, 0, 255, 0));
  border-radius: 999px;
  filter: drop-shadow(0 0 6px #699bff);
  -webkit-animation: tail 3000ms ease-in-out infinite, shooting 3000ms ease-in-out infinite;
          animation: tail 3000ms ease-in-out infinite, shooting 3000ms ease-in-out infinite;
}
.shooting-star::before {
  content: "";
  position: absolute;
  top: calc(50% - 1px);
  right: 0;
  height: 2px;
  background: linear-gradient(-45deg, rgba(0, 0, 255, 0), #5f91ff, rgba(0, 0, 255, 0));
  transform: translateX(50%) rotateZ(45deg);
  border-radius: 100%;
  -webkit-animation: shining 3000ms ease-in-out infinite;
          animation: shining 3000ms ease-in-out infinite;
}
.shooting-star::after {
  content: "";
  position: absolute;
  top: calc(50% - 1px);
  right: 0;
  height: 2px;
  background: linear-gradient(-45deg, rgba(0, 0, 255, 0), #5f91ff, rgba(0, 0, 255, 0));
  transform: translateX(50%) rotateZ(45deg);
  border-radius: 100%;
  -webkit-animation: shining 3000ms ease-in-out infinite;
          animation: shining 3000ms ease-in-out infinite;
  transform: translateX(50%) rotateZ(-45deg);
}
.shooting-star:nth-child(1) {
  top: calc(50% - -74px);
  left: calc(50% - 161px);
  -webkit-animation-delay: 4612ms;
          animation-delay: 4612ms;
}
.shooting-star:nth-child(1)::before, .shooting-star:nth-child(1)::after {
  -webkit-animation-delay: 4612ms;
          animation-delay: 4612ms;
}
.shooting-star:nth-child(2) {
  top: calc(50% - 196px);
  left: calc(50% - 203px);
  -webkit-animation-delay: 9837ms;
          animation-delay: 9837ms;
}
.shooting-star:nth-child(2)::before, .shooting-star:nth-child(2)::after {
  -webkit-animation-delay: 9837ms;
          animation-delay: 9837ms;
}
.shooting-star:nth-child(3) {
  top: calc(50% - -150px);
  left: calc(50% - 255px);
  -webkit-animation-delay: 1760ms;
          animation-delay: 1760ms;
}
.shooting-star:nth-child(3)::before, .shooting-star:nth-child(3)::after {
  -webkit-animation-delay: 1760ms;
          animation-delay: 1760ms;
}
.shooting-star:nth-child(4) {
  top: calc(50% - 174px);
  left: calc(50% - 83px);
  -webkit-animation-delay: 1171ms;
          animation-delay: 1171ms;
}
.shooting-star:nth-child(4)::before, .shooting-star:nth-child(4)::after {
  -webkit-animation-delay: 1171ms;
          animation-delay: 1171ms;
}
.shooting-star:nth-child(5) {
  top: calc(50% - -87px);
  left: calc(50% - 104px);
  -webkit-animation-delay: 1124ms;
          animation-delay: 1124ms;
}
.shooting-star:nth-child(5)::before, .shooting-star:nth-child(5)::after {
  -webkit-animation-delay: 1124ms;
          animation-delay: 1124ms;
}
.shooting-star:nth-child(6) {
  top: calc(50% - 40px);
  left: calc(50% - 217px);
  -webkit-animation-delay: 1869ms;
          animation-delay: 1869ms;
}
.shooting-star:nth-child(6)::before, .shooting-star:nth-child(6)::after {
  -webkit-animation-delay: 1869ms;
          animation-delay: 1869ms;
}
.shooting-star:nth-child(7) {
  top: calc(50% - 127px);
  left: calc(50% - 61px);
  -webkit-animation-delay: 6558ms;
          animation-delay: 6558ms;
}
.shooting-star:nth-child(7)::before, .shooting-star:nth-child(7)::after {
  -webkit-animation-delay: 6558ms;
          animation-delay: 6558ms;
}
.shooting-star:nth-child(8) {
  top: calc(50% - -192px);
  left: calc(50% - 103px);
  -webkit-animation-delay: 3556ms;
          animation-delay: 3556ms;
}
.shooting-star:nth-child(8)::before, .shooting-star:nth-child(8)::after {
  -webkit-animation-delay: 3556ms;
          animation-delay: 3556ms;
}
.shooting-star:nth-child(9) {
  top: calc(50% - -151px);
  left: calc(50% - 162px);
  -webkit-animation-delay: 5542ms;
          animation-delay: 5542ms;
}
.shooting-star:nth-child(9)::before, .shooting-star:nth-child(9)::after {
  -webkit-animation-delay: 5542ms;
          animation-delay: 5542ms;
}
.shooting-star:nth-child(10) {
  top: calc(50% - -103px);
  left: calc(50% - 100px);
  -webkit-animation-delay: 5156ms;
          animation-delay: 5156ms;
}
.shooting-star:nth-child(10)::before, .shooting-star:nth-child(10)::after {
  -webkit-animation-delay: 5156ms;
          animation-delay: 5156ms;
}
.shooting-star:nth-child(11) {
  top: calc(50% - -119px);
  left: calc(50% - 147px);
  -webkit-animation-delay: 1146ms;
          animation-delay: 1146ms;
}
.shooting-star:nth-child(11)::before, .shooting-star:nth-child(11)::after {
  -webkit-animation-delay: 1146ms;
          animation-delay: 1146ms;
}
.shooting-star:nth-child(12) {
  top: calc(50% - -46px);
  left: calc(50% - 139px);
  -webkit-animation-delay: 3940ms;
          animation-delay: 3940ms;
}
.shooting-star:nth-child(12)::before, .shooting-star:nth-child(12)::after {
  -webkit-animation-delay: 3940ms;
          animation-delay: 3940ms;
}

@-webkit-keyframes tail {
  0% {
    width: 0;
  }
  30% {
    width: 100px;
  }
  100% {
    width: 0;
  }
}

@keyframes tail {
  0% {
    width: 0;
  }
  30% {
    width: 100px;
  }
  100% {
    width: 0;
  }
}
@-webkit-keyframes shining {
  0% {
    width: 0;
  }
  50% {
    width: 30px;
  }
  100% {
    width: 0;
  }
}
@keyframes shining {
  0% {
    width: 0;
  }
  50% {
    width: 30px;
  }
  100% {
    width: 0;
  }
}
@-webkit-keyframes shooting {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(300px);
  }
}
@keyframes shooting {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(300px);
  }
}
@-webkit-keyframes sky {
  0% {
    transform: rotate(45deg);
  }
  100% {
    transform: rotate(405deg);
  }
}
@keyframes sky {
  0% {
    transform: rotate(45deg);
  }
  100% {
    transform: rotate(405deg);
  }
}

img {
  max-width: 100%;
}
.bulb-container {
  font-size: 1rem;
  perspective: 800px;
  position: absolute;
  z-index: 99;
  padding-top: 0.5em;
  margin-bottom: 0.5em;
  top: 0;
  right: 20px;
}
.bulb-container::after {
  content: "";
  width: 1.125em;
  height: 0.5em;
  background: url(//www.w3cplus.com/sites/default/files/blogs/2020/2002/bulb-top.png);
  background-size: 100% 100%;
  position: absolute;
  left: calc(50% - 0.5625em);
  top: 0;
}

.bulb {
  font-size: 1rem;
  width: 3.375em;
  height: 11.5em;
  margin: 0 auto;
  transform-origin: center top;
  animation: swing 3s ease-in-out infinite alternate;
  position: relative;
  transform-style: preserve3d;
  transition: transform 0.5s ease-out;
  cursor: pointer;
  display: block;
  background: none;
  border: none;
  -webkit-appearance: none;
  padding: 0;
}
.bulb:focus {
  outline-offset: 1rem;
  outline: none;
}

.bulb:hover .bulb__image img,
.bulb:focus .bulb__image img,
.bulb:active .bulb__image img {
  outline: none;
  animation: flicker 2s linear infinite alternate;
}

.bulb:hover .bulb__image::before,
.bulb:focus .bulb__image::before,
.bulb:active .bulb__image::before {
  outline: none;
  animation: flicker-light 2s linear infinite alternate;
}

.bulb__image {
  outline: none;
  transform-style: preserve3d;
  display: block;
  transform-origin: center top;
  animation: scale 2.5s -1.5s ease-in-out infinite alternate;
  position: relative;
}
.bulb__image::before {
  content: "";
  position: absolute;
  left: calc(50% - 1px);
  bottom: 0;
  width: 0.625em;
  height: 0.625em;
  background: transparent;
  border-radius: 50%;
  z-index: -1;
  box-shadow: 0 0 6.375em 4em rgb(160, 131, 3);
  opacity: 0.6;
  transform: scaleY(0.7) translateY(-1em) translateX(0.4em);
  transform-origin: center top;
}

.bulb__image img {
  display: block;
  /* filter: saturate(0); */
  filter: hue-rotate(236deg);
  width: 3.375em;
}

@keyframes swing {
  0% {
    transform: rotate(4deg);
  }

  100% {
    transform: rotate(-4deg);
  }
}

@keyframes scale {
  0% {
    transform: scale(0.98);
  }

  100% {
    transform: scale(1.02);
  }
}

@keyframes flicker {
  0%,
  4%,
  8%,
  12%,
  20%,
  30%,
  40%,
  50%,
  100% {
    filter: saturate(0);
  }

  2%,
  6%,
  10% {
    filter: saturate(1.4);
  }

  25%,
  35%,
  45% {
    filter: saturate(1.6);
  }

  80% {
    filter: saturate(3);
  }
}

@keyframes flicker-light {
  0%,
  4%,
  8%,
  12%,
  20%,
  30%,
  40%,
  50%,
  100% {
    filter: saturate(0);
    opacity: 0.5;
  }

  2%,
  6%,
  10% {
    filter: saturate(1.4);
    opacity: 0.6;
  }

  25%,
  35%,
  45% {
    filter: saturate(1.6);
    opacity: 0.6;
  }

  80% {
    filter: saturate(3);
    opacity: 0.7;
  }
}
</style>