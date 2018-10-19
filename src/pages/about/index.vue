<template>
  <div class="container">
  </div>
</template>
<script>
export default {
  data () {
    return {
    }
  },
  components: {
    // card
  },

  methods: {
    setNavigationBarColor(color){
      wx.setNavigationBarColor({
        frontColor: '#ffffff',
        backgroundColor: '',
      })
    },
  },

  mounted () {
    // 调用应用实例的方法获取全局数据
    this.setNavigationBarColor();
  }
}
</script>

<style scoped>
.container{
  display:flex;
  flex-direction:column;
  min-height:100vh;
  color:#fff;
  font-size:30rpx;
  /* position: absolute; */
}
.bcg{
  position:fixed;
  z-index:2;
  height:100%;
  width:100%;
  top:0px;
  right:0;
  bottom:0;
  left:0;
}
.sear{
  color: #fff;
  z-index: 2;
  border-bottom: 1px solid #fff;
  margin: 15rpx 50rpx;
}
.sear img{
  width:28rpx;
  height:28rpx;
  margin-right:16rpx;
  vertical-align: text-top;
  margin: 0 15rpx;

}
.input_sty{
  display: inline-block;
}
.content{
  position: relative;
  z-index: 2;
  padding: 15rpx 50rpx;
}
.weather_info{
  text-align: center;
  padding-bottom:50rpx;

}
.temp{
  height: 360rpx;
  font-size: 200rpx;
  line-height: 360rpx;
}
.weather{
  margin-bottom:30rpx;
}
.pm{
  font-size:24rpx;
  height:1em;
  line-height:1em;
  padding:10rpx 20rpx;
  border-radius:20rpx;
  background:rgba(240, 240, 240, .2);

}
.guide{
  background: rgba(0,0,0,0.6);
  margin: 0 -50rpx;
  font-size: 24rpx;
  display: flex;
  justify-content:space-around;
  text-align: center;
  padding-top: 20rpx;
  margin-bottom: 20rpx;
}
.guide .item div{
  margin-bottom: 20rpx;
}
.livingIndex{
  background:rgba(0,0,0,0.6);
  margin: 0 -50rpx;

}
.livingIndex .item{
  display: flex;
  justify-content: space-around;
  align-items: center;
  border-bottom: 1rpx solid #ccc;
  padding-bottom: 20rpx;
  margin-left: 50rpx;
  margin-right: 50rpx;
  padding-top: 20rpx;
}
.icon{
  width:80rpx;
  height:80rpx;
  padding-right: 24rpx;
  flex-shrink: 0;
}
.right p:last-child{
  font-size: 24rpx;
  margin-top:10rpx; 
}
.footer{
  display:flex;
  justify-content:space-around;
  align-items:center;
  height:60rpx;
  font-size:22rpx;
  color:#fff;
  z-index:3;
}
.menu_sty{

}
</style>
