<template>
  <div class="container">
    <image class='bcg' src="/static/fog-himalayas-landscape-38326.jpg" mode='aspectFill'/>
    <div class="sear">
      <img src="../../img/search.png"/>
      <input class="input_sty" placeholder="查询其他城市天气"/>
    </div>
    <!-- 主体部分 -->
    <div class="content">
      <div>头像 - 用户名</div>
      <div style="display:flex;justify-content:space-between;">
        <span style="font-size:62rpx;">上海市</span>
        <span style="font-size:22rpx">10-15 17:11 更新</span>
      </div>
      <div style="font-size:22rpx; margin-top:30rpx;">
        下午好，长时间敲代码，能让你的腰间盘更加突出噢
      </div>
      <div class="weather_info">
        <div class="temp">16°</div>
        <div class="weather">小雨转多云</div>
        <span class="pm">优 30</span>
      </div>
      <div class="guide">
        <div class="item" v-for="(item,index) in 4" :key="index">
          <div>今天</div>
          <div>21~25°</div>
          <div>小雨转多云</div>
          <div>东北风微风</div>
        </div>
      </div>
      <div class="livingIndex">
        <div class="item" v-for="(item,index) in 5" :key="index" v-bind:style="{ 'border': index+1==5 ? '0':''}">
          <img src="/static/clothing.png" class="icon"/>
          <div class="right">
            <p>穿衣指数 较舒适</p>
            <p>建议着薄外套、开衫牛仔衫裤等服装。年老体弱者应适当添加衣物，宜着夹克衫、薄毛衣等。</p>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">开发者：cxl</div>
    <!-- 右侧点击图标 -->
    <div class="menu_sty">
      <img src="/static/menu.png" style="height:40px;width:40px;"/>
    </div>
  </div>
</template>
<script>
import card from '@/components/card'
export default {
  data () {
    return {
      motto: 'Hello World',
      userInfo: {},
      weatherData:'555',
      bcgImgList: [
      {
        src: '/img/beach-bird-birds-235787.jpg',
        topColor: '#393836'
      },
      {
        src: '/img/clouds-forest-idyllic-417102.jpg',
        topColor: '#0085e5'
      },
      {
        src: '/img/backlit-dawn-dusk-327466.jpg',
        topColor: '#2d2225'
      },
      {
        src: '/img/accomplishment-adventure-clear-sky-585825.jpg',
        topColor: '#004a89'
      },
      {
        src: '/img/fog-himalayas-landscape-38326.jpg',
        topColor: '#b8bab9'
      },
      {
        src: '/img/asphalt-blue-sky-clouds-490411.jpg',
        topColor: '#009ffe'
      },
      {
        src: '/img/aerial-climate-cold-296559.jpg',
        topColor: '#d6d1e6'
      },
      {
        src: '/img/beautiful-cold-dawn-547115.jpg',
        topColor: '#ffa5bc'
      }
    ],
    }
  },
  components: {
    card
  },

  methods: {
    initFun(){},
    setNavigationBarColor(color){
      wx.setNavigationBarColor({
        frontColor: '#ffffff',
        backgroundColor: '#b8bab9',
      })
    },
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
    this.initFun()
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
position:fixed;
right:70rpx;
bottom:150rpx;
z-index:100;

}
</style>
