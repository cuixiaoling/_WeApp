<template>
  <div class="counter-warp">
   <div :animation="animationData" style="background:red;height:100rpx;width:100rpx"></div>
   <div @click="fun1">点击</div>
  </div>
</template>

<script>
export default {
  data(){
    return{
       animationData: {},
       animation:{}
    }
  },
  methods: {
    rotateAndScale() {
      console.log('旋转同时放大')
      // 旋转同时放大
      this.animation.rotate(45).scale(2, 2).step()
      this.animationData=  this.animation.export();
    },
    rotateThenScale() {
      // 先旋转后放大
      this.animation.rotate(45).step()
      this.animation.scale(2, 2).step()
      this.animationData=  this.animation.export();
    },
    rotateAndScaleThenTranslate: function () {
      // 先旋转同时放大，然后平移
      this.animation.rotate(45).scale(2, 2).step()
      this.animation.translate(100, 100).step({ duration: 1000 })
      this.animationData=  this.animation.export();

    },
    fun1(){
      console.log('xixxixi')
      this.animation.rotate(45).scale(2, 2).step()
      this.animationData=  this.animation.export();
    }
  },
  created(){},
  mounted(){
    var animation = wx.createAnimation({
      duration: 1000,
  	  timingFunction: 'ease',
    })
    this.animation = animation
    animation.scale(2,2).rotate(45).step()
    this.animationData=animation.export()
    setTimeout(function() {
      animation.translate(30).step()
      this.animationData=animation.export()
    }.bind(this), 1000)
  }
}
</script>

<style>
.counter-warp {
  text-align: center;
  margin-top: 100px;
}
.home {
  display: inline-block;
  margin: 100px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
