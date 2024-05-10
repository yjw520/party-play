<template>
  <!-- <view :animation="animationData" style="background:red;height:100rpx;width:100rpx"></view> -->
  <view class="">
  	敬情期待
  </view>
</template>

<script>
export default{
  data() {
    return {
      animationData: {},
	  timer: null,
    }
  },
  // onShow: function(){
  //   var animation = uni.createAnimation({
		// timingFunction: 'linear',
  //   })
	 // this.animation = animation
		// const f = () => {
		// 	animation.translateX('500px').step({
		// 		duration: 4000,
		// 	});
			
		// 	this.animationData = this.animation.export();
		// 	this.timer = setTimeout(() => {
		// 		this.animation.translateX('-100px').step({
		// 			duration: 0
		// 		});
		// 		this.animationData = this.animation.export();
		// 	}, 4000);
		// };
		// f();
		// setInterval(f, 4500);
  // },
  // onUnload() {
  // 	clearInterval(this.timer);
  // },
  methods:{
    // rotateAndScale: function () {
    //   // 旋转同时放大
    //   this.animation.rotate(45).scale(2, 2).step()
    //   this.animationData = this.animation.export()
    // },
    // rotateThenScale: function () {
    //   // 先旋转后放大
    //   this.animation.rotate(45).step()
    //   this.animation.scale(2, 2).step()
    //   this.animationData = this.animation.export()
    // },
    // rotateAndScaleThenTranslate: function () {
    //   // 先旋转同时放大，然后平移
    //   this.animation.rotate(45).scale(2, 2).step()
    //   this.animation.translate(100, 100).step({ duration: 1000 })
    //   this.animationData = this.animation.export()
    // }
  }
}
</script>
