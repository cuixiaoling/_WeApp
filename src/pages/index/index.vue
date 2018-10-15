<template>
  <div class="container">
    <image class='bcg' src="../../img/beach-bird-birds-235787.jpg" mode='aspectFill'></image>
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
        backgroundColor: '#393836',
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
  font-size:30rpx
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
</style>
