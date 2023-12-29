<template>
  <view :animation="animationData" style="background:red;height:100rpx;width:100rpx"></view>
</template>

<script>
export default{
  data() {
    return {
      animationData: {},
	  timer: null,
    }
  },
  onShow: function(){
    var animation = uni.createAnimation({
		
		// duration: 1000,
		timingFunction: 'linear',
    })
	 this.animation = animation
		
		const f = () => {
			console.log('======>f');
			console.log(Date.now());
			animation.translateX('500px').step({
				duration: 4000,
			});
			
			this.animationData = this.animation.export();
			
			
			
			this.timer = setTimeout(() => {
				this.animation.translateX('-100px').step({
					duration: 0
				});
				this.animationData = this.animation.export();
				// f();
				console.log(Date.now());
			}, 4000);
		};
		f();
		setInterval(f, 4500);
		// if (this.timer) {
		//     clearTimeout(this.timer);
		// }
		// this.timer = setInterval(() => {
		// 	f();
		// }, 5000)
		// this.animationData = this.animation.export();

   //  animation.scale(2,2).rotate(45).step()

   //  this.animationData = animation.export()

   //  this.timer = setInterval(function() {
   //    animation.translate(30).step()
   //    this.animationData = animation.export()
	  // console.log(22222);
	  // // animation.translate(0).step()
	  // // this.animationData = animation.export()
   //  }.bind(this), 1000)
	// setInterval(() => {
	// 	animation.translate(0).step()
	// 	this.animationData = animation.export()
	// }, 2000)
	// setTimeout(function() {
	// 	animation.translate(0).step()
	// 	this.animationData = animation.export()
	// }.bind(this), 2000)
  },
  onUnload() {
  	clearInterval(this.timer);
  },
  methods:{
    rotateAndScale: function () {
      // 旋转同时放大
      this.animation.rotate(45).scale(2, 2).step()
      this.animationData = this.animation.export()
    },
    rotateThenScale: function () {
      // 先旋转后放大
      this.animation.rotate(45).step()
      this.animation.scale(2, 2).step()
      this.animationData = this.animation.export()
    },
    rotateAndScaleThenTranslate: function () {
      // 先旋转同时放大，然后平移
      this.animation.rotate(45).scale(2, 2).step()
      this.animation.translate(100, 100).step({ duration: 1000 })
      this.animationData = this.animation.export()
    }
  }
}
</script>
