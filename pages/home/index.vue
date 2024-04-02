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
			<u-notice-bar text="你在干什么？在吃香菜"></u-notice-bar>
		</view>
		<view class="swiper-wrap">
			<u-swiper
				:list="swiperList"
				indicator
				indicatorMode="line"
				circular
				duration="1000"
			></u-swiper>
		</view>
		<view class="">
			<u-transition :show="show" mode="slide-right">
			<div class="card" style="--color: #00afaf">
				<button class="button" @click="goGuessCate">
					<span class="text">你演我猜</span>
					<div class="icon">
						<image src="../../static/image/barrage.png" mode=""></image>
					</div>
				</button>
			</div>
			</u-transition>
			<u-transition :show="show" mode="slide-left">
			<div class="card" style="--color: #00bb00">
			  <button class="button" @click="goBarrage">
				<span class="text">手持弹幕</span>
				<div class="icon">
				  <svg>
					<use xlink:href="#arrow-right"></use>
				  </svg>
				</div>
			  </button>
			</div>
			</u-transition>
			<u-transition :show="show" mode="slide-right">
			<div class="card" style="--color: #0f2bff">
			  <button class="button" @click="goBarrage2">
				<span class="text">Hover</span>
				<div class="icon">
				  <svg>
					<use xlink:href="#arrow-right"></use>
				  </svg>
				</div>
			  </button>
			</div>
			</u-transition>
		</view>
	</view>
</template>

<script>
	 import BarrageIcon from '../icon/barrage.vue';
	 export default {
		 components: {
			 BarrageIcon,
		 },
	        data() {
	            return {
	                show: true,
					swiperList: [
						'https://raw.githubusercontent.com/mobalti/open-props-interfaces/main/dropdown-menu/images/img-3-desktop.webp',
						'https://raw.githubusercontent.com/mobalti/open-props-interfaces/main/dropdown-menu/images/img-2-desktop.webp',
						'https://raw.githubusercontent.com/mobalti/open-props-interfaces/main/dropdown-menu/images/img-4-desktop.webp',
						'https://raw.githubusercontent.com/mobalti/open-props-interfaces/main/dropdown-menu/images/img-5-desktop.webp',
						'https://raw.githubusercontent.com/mobalti/open-props-interfaces/main/dropdown-menu/images/img-1-desktop.webp'
					]
	            }
	        },
			methods: {
				goGuessCate() {
					// uni.navigateTo({
					// 	url: '/pages/guess-category/index',
					// });
					uni.navigateTo({
						url: '/pages/test/index',
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
					});
				}
			},
			onShow() {
				this.show = true;
			},
			onHide() {
				this.show = false;
			}
	    }
</script>

<style lang="scss">
.home-wrap {
	background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
	height: 100vh;
	// overflow: hidden;
	overflow: scroll;
	.swiper-wrap {
		margin: 22rpx 26rpx;
	}
}
.night-wrap {
	position: absolute;
}
.night {
  width: 300rpx;
  height: 600rpx;
  transform: rotateZ(45deg);
}

.shooting-star {
  position: absolute;
  left: 50%;
  top: 50%;
  height: 4rpx;
  background: linear-gradient(-45deg, #5f91ff, rgba(0, 0, 255, 0));
  border-radius: 1998rpx;
  filter: drop-shadow(0 0 6px #699bff);
  -webkit-animation: tail 3000ms ease-in-out infinite, shooting 3000ms ease-in-out infinite;
          animation: tail 3000ms ease-in-out infinite, shooting 3000ms ease-in-out infinite;
}
.shooting-star::before {
  content: "";
  position: absolute;
  top: calc(50% - 2rpx);
  right: 0;
  height: 4rpx;
  background: linear-gradient(-45deg, rgba(0, 0, 255, 0), #5f91ff, rgba(0, 0, 255, 0));
  transform: translateX(50%) rotateZ(45deg);
  border-radius: 100%;
  -webkit-animation: shining 3000ms ease-in-out infinite;
          animation: shining 3000ms ease-in-out infinite;
}
.shooting-star::after {
  content: "";
  position: absolute;
  top: calc(50% - 1rpx);
  right: 0;
  height: 4rpx;
  background: linear-gradient(-45deg, rgba(0, 0, 255, 0), #5f91ff, rgba(0, 0, 255, 0));
  transform: translateX(50%) rotateZ(45deg);
  border-radius: 100%;
  -webkit-animation: shining 3000ms ease-in-out infinite;
          animation: shining 3000ms ease-in-out infinite;
  transform: translateX(50%) rotateZ(-45deg);
}
.shooting-star:nth-child(1) {
  top: calc(50% - -148rpx);
  left: calc(50% - 222rpx);
  -webkit-animation-delay: 4612ms;
          animation-delay: 4612ms;
}
.shooting-star:nth-child(1)::before, .shooting-star:nth-child(1)::after {
  -webkit-animation-delay: 4612ms;
          animation-delay: 4612ms;
}
.shooting-star:nth-child(2) {
  top: calc(50% - 292rpx);
  left: calc(50% - 406rpx);
  -webkit-animation-delay: 9837ms;
          animation-delay: 9837ms;
}
.shooting-star:nth-child(2)::before, .shooting-star:nth-child(2)::after {
  -webkit-animation-delay: 9837ms;
          animation-delay: 9837ms;
}
.shooting-star:nth-child(3) {
  top: calc(50% - -300rpx);
  left: calc(50% - 510rpx);
  -webkit-animation-delay: 1760ms;
          animation-delay: 1760ms;
}
.shooting-star:nth-child(3)::before, .shooting-star:nth-child(3)::after {
  -webkit-animation-delay: 1760ms;
          animation-delay: 1760ms;
}
.shooting-star:nth-child(4) {
  top: calc(50% - 248rpx);
  left: calc(50% - 166rpx);
  -webkit-animation-delay: 1171ms;
          animation-delay: 1171ms;
}
.shooting-star:nth-child(4)::before, .shooting-star:nth-child(4)::after {
  -webkit-animation-delay: 1171ms;
          animation-delay: 1171ms;
}
.shooting-star:nth-child(5) {
  top: calc(50% - -174rpx);
  left: calc(50% - 208rpx);
  -webkit-animation-delay: 1124ms;
          animation-delay: 1124ms;
}
.shooting-star:nth-child(5)::before, .shooting-star:nth-child(5)::after {
  -webkit-animation-delay: 1124ms;
          animation-delay: 1124ms;
}
.shooting-star:nth-child(6) {
  top: calc(50% - 80rpx);
  left: calc(50% - 434rpx);
  -webkit-animation-delay: 1869ms;
          animation-delay: 1869ms;
}
.shooting-star:nth-child(6)::before, .shooting-star:nth-child(6)::after {
  -webkit-animation-delay: 1869ms;
          animation-delay: 1869ms;
}
.shooting-star:nth-child(7) {
  top: calc(50% - 254rpx);
  left: calc(50% - 122rpx);
  -webkit-animation-delay: 6558ms;
          animation-delay: 6558ms;
}
.shooting-star:nth-child(7)::before, .shooting-star:nth-child(7)::after {
  -webkit-animation-delay: 6558ms;
          animation-delay: 6558ms;
}
.shooting-star:nth-child(8) {
  top: calc(50% - -384rpx);
  left: calc(50% - 206rpx);
  -webkit-animation-delay: 3556ms;
          animation-delay: 3556ms;
}
.shooting-star:nth-child(8)::before, .shooting-star:nth-child(8)::after {
  -webkit-animation-delay: 3556ms;
          animation-delay: 3556ms;
}
.shooting-star:nth-child(9) {
  top: calc(50% - -302px);
  left: calc(50% - 324px);
  -webkit-animation-delay: 5542ms;
          animation-delay: 5542ms;
}
.shooting-star:nth-child(9)::before, .shooting-star:nth-child(9)::after {
  -webkit-animation-delay: 5542ms;
          animation-delay: 5542ms;
}
.shooting-star:nth-child(10) {
  top: calc(50% - -206rpx);
  left: calc(50% - 200rpx);
  -webkit-animation-delay: 5156ms;
          animation-delay: 5156ms;
}
.shooting-star:nth-child(10)::before, .shooting-star:nth-child(10)::after {
  -webkit-animation-delay: 5156ms;
          animation-delay: 5156ms;
}
.shooting-star:nth-child(11) {
  top: calc(50% - -238rpx);
  left: calc(50% - 294rpx);
  -webkit-animation-delay: 1146ms;
          animation-delay: 1146ms;
}
.shooting-star:nth-child(11)::before, .shooting-star:nth-child(11)::after {
  -webkit-animation-delay: 1146ms;
          animation-delay: 1146ms;
}
.shooting-star:nth-child(12) {
  top: calc(50% - -92rpx);
  left: calc(50% - 278px);
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
    width: 200rpx;
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
    width: 200rpx;
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
    width: 60rpx;
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
    width: 60rpx;
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
    transform: translateX(600rpx);
  }
}
@keyframes shooting {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(600rpx);
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
  perspective: 1600rpx;
  position: absolute;
  z-index: 99;
  padding-top: 0.5em;
  margin-bottom: 0.5em;
  top: 0;
  right: 40rpx;
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
  // width: 1.6875em;
  // height: 11.5em;
  height: 15em;
  // height: 5.75em;
  // width: 6.75rpx;
  // height: 23rpx;
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


.card {
	position: relative;
	display: flex;
	justify-content: center;
	align-items: center;
	height: 250rpx;
	margin: 10px;
	background: linear-gradient(rgba(25, 31, 50, 0.2), rgba(4, 8, 20, 0.01)),
		rgba(4, 8, 20, 0.8);
	box-shadow: inset 0 0 0 1px rgba(200, 200, 220, 0.16),
		inset 0 0 5px -3px var(--color), inset 0 12px 48px 0 rgba(160, 220, 240, 0.08),
		inset 0 0 120px -100px var(--color);
	border-radius: 16px;
	color: var(--color);
	overflow: hidden;
	.button {
		--w: 180px;
		--h: 60px;
		--icon-size: 25px;
		--text-color: rgb(210 210 240);
		--box-glow-color: transparent;
		--box-glow-blur: 20px;
		position: relative;
		min-width: var(--w);
		min-height: var(--h);
		border-radius: var(--h);
		display: flex;
		justify-content: center;
		align-items: center;
		border: none;
		font-family: "Montserrat";
		color: var(--text-color);
		background: rgba(4, 8, 20, 0.8);
		box-shadow: 0px 0px 0px 1px rgba(200, 200, 220, 0.22),
			0px 0px var(--box-glow-blur) var(--box-glow-color),
			inset 0 0 26px -10px var(--box-glow-color);
		overflow: hidden;
		cursor: pointer;
		transition: box-shadow 500ms ease;
		z-index: 2;
	}
	.button::before {
		content: "";
		position: absolute;
		inset: 0;
		background: rgba(200, 200, 220, 0.1);
		box-shadow: inset 0 0px 24px 0 rgba(170, 230, 250, 0.12);
		border-radius: var(--h);
		z-index: 1;
		transition: transform 500ms ease, box-shadow 500ms ease;
	}
	.button:active {
		--box-glow-blur: 36px;
	}
	.button:hover,
	.button:active {
		--box-glow-color: var(--color);
	}
	.button:hover::before,
	.button:active::before {
		transform: translateX(65%);
		box-shadow: inset 0 0px 0px 0 transparent;
	}
	.button:hover .text,
	.button:active .text {
		transform: translateX(0%);
		animation-play-state: running;
	}
	.button:hover .icon,
	.button:active .icon {
		transform: translateX(calc(var(--w) - var(--icon-size) - 19px));
		color: var(--color);
	}
	
	.button:focus-visible {
		outline: none;
	}
	.button:focus-visible:not(:hover, :active) {
		--box-glow-color: rgba(114, 114, 114, 0.5);
	}
	.text,
	.icon {
		z-index: 2;
	}
	.icon {
		position: absolute;
		// width: var(--icon-size);
		// height: var(--icon-size);
		width: 25px;
		height: 25px;
		left: 0;
		transform: translateX(calc((var(--w)) / 2 + 8px));
		transition: transform 500ms ease, color 500ms ease;
	}
	.text {
		transform: translateX(-50%);
		font-family: "Montserrat";
		transition: transform 500ms ease;
	}
	
}
.card::before {
	content: "";
	position: absolute;
	inset: 0;
	background-image: radial-gradient(var(--color) 8%, transparent 8%),
		radial-gradient(var(--color) 8%, transparent 8%),
		radial-gradient(var(--color) 8%, transparent 8%),
		radial-gradient(var(--color) 8%, transparent 8%);
	background-position: 0% 0%, 0% 100%, 100% 0%, 100% 100%;
	background-size: 40px 40px;
	background-repeat: no-repeat;
	filter: drop-shadow(0 0 6px var(--color));
}
.card::after {
	content: "";
	position: absolute;
	inset: 0;
	background-color: var(--color);
	opacity: 0.2;
	-webkit-mask-image: radial-gradient(90% 90% at 50% 50%, transparent, black);
	mask-image: radial-gradient(90% 90% at 50% 50%, transparent, black);
	filter: url(#noiseFilter);
	z-index: 1;
}
</style>