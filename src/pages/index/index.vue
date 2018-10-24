<template>
  <div class="container">
    <image class='bcg' src="/static/fog-himalayas-landscape-38326.jpg" mode='aspectFill'/>
    <div class="sear" v-if="!!setting.hiddenSearch">
      <img src="../../img/search.png"/>
      <input class="input_sty" placeholder="查询其他城市天气" v-model="searchVal" @confirm="confirm($event)" @blur="searchFun"/>
    </div>
    <!-- 主体部分 -->
    <div class="content">
      <div class="avatarInfo">
          <open-data class='avatar' type='userAvatarUrl'></open-data>
          <open-data class='name' type='userNickName'></open-data>
          <img class='downArrow' src='/static/down-arrow.png'/>
      </div>
      <div style="display:flex;justify-content:space-between;">
        <span style="font-size:62rpx;">{{cityDatas.basic.location || '定位中'}}</span>
        <span style="font-size:22rpx">{{cityDatas.updateTimeFormat}}更新</span>
      </div>
      <div style="font-size:22rpx; margin-top:30rpx;">
        下午好，长时间敲代码，能让你的腰间盘更加突出噢<div>{{!!setting.hiddenSearch}}</div>
      </div>
      <div class="weather_info">
        <div class="temp">{{cityDatas.now.tmp || '-'}}<span style="font-size:50rpx;position:relative; top:-50px;">℃</span></div>
        <div class="weather">{{cityDatas.now.cond_txt || '--'}}</div>
        <span class="pm">能见度 {{cityDatas.now.vis}}</span>
      </div>
      <div class="guide">
        <div class="item" v-for="(item,index) in cityDatas.daily_forecast" :key="index">
          <div>{{item.date}}</div>
          <div>{{item.tmp_min}}~{{item.tmp_max}}℃</div>
          <div>{{item.cond_txt_d}}</div>
          <div>{{item.wind_dir}}</div>
        </div>
      </div>
      <div class="livingIndex" v-if="!!hiddenIndex">
        <div class="item" v-for="(item,index) in cityDatas.lifestyle" :key="index" v-bind:style="{ 'border': index+1==5 ? '0':''}">
          <img src='/static/lifestyle_ac.png' class="icon"/>
          <div class="right">
            <p>{{lifestyles[item.type]}} {{item.brf}}</p>
            <p>{{item.txt}}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">开发者：cxl</div>
    <!-- 右侧点击图标 -->
    <div class="menu_sty">
      <img src="/static/location.png" :animation="animationOne"  @click="menuOne" class="pos_icon opcition0"/>
      <img src="/static/setting.png" :animation="animationTwo" @click="menuTwo" class="pos_icon opcition0"/>
      <img src="/static/info.png" :animation="animationThree" @click="menuThree" class="pos_icon opcition0"/>
      <img @click="menuMain" :animation="animationMain" src="/static/menu.png" class="pos_icon"/>
    </div>
  </div>
</template>
<script>
import card from '@/components/card'
const key = '4675b2eed06e4074b06744d153db6941'
export default {
  data () {
    return {
      setting:{},
      motto: 'Hello World',
      userInfo: {},
      weatherData:'555',
      show:false,
      // 是否已经弹出
      hasPopped: false,
      animationMain: {},
      animationOne: {},
      animationTwo: {},
      animationThree: {},
      // 天气预报
      cityDatas:{},
      noWeater:{},
      liftSty:{},
      searchVal:"",//搜索的内容
      lifestyles: {
      'comf': '舒适度指数',
      'cw': '洗车指数',
      'drsg': '穿衣指数',
      'flu': '感冒指数',
      'sport': '运动指数',
      'trav': '旅游指数',
      'uv': '紫外线指数',
      'air': '空气污染扩散条件指数',
      'ac': '空调开启指数',
      'ag': '过敏指数',
      'gl': '太阳镜指数',
      'mu': '化妆指数',
      'airc': '晾晒指数',
      'ptfc': '交通指数',
      'fsh': '钓鱼指数',
      'spi': '防晒指数',
    },
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
    initSetting(){
      wx.getStorage({
        key:'setting',
        success:(res)=>{
          let setting = res.data || {}
          this.setting = setting;
          console.log(this.setting.hiddenSearch)
        },
        fail:()=>{
          this.setting = {}
        }
      })
    },
    confirm(e) {
      console.log(e)
    },
    menuTwo(){
      wx.navigateTo({
        url:'../setting/main'
      })
    },
    searchFun:function(){
      console.log('vue-失去焦点')
      this.searchVal;
      this.getWeather(this.searchVal);
    },
    setNavigationBarColor(color){
      wx.setNavigationBarColor({
        frontColor: '#ffffff',
        backgroundColor: '#b8bab9',
      })
     
    },
    // 点击主菜单
    menuMain(){
      this.show = true;
      if(this.hasPopped){
        this.takeback()
      }
      else
      {
          this.popp()
      }
    },

    // 弹出子菜单
    popp(){
      let animationMain = wx.createAnimation({
        duration: 200,
        timingFunction: 'ease-out'
      })
      let animationOne = wx.createAnimation({
        duration: 200,
        timingFunction: 'ease-out'
      })
      let animationTwo = wx.createAnimation({
        duration: 200,
        timingFunction: 'ease-out'
      })
      let animationThree = wx.createAnimation({
        duration: 200,
        timingFunction: 'ease-out'
      })
      animationMain.rotateZ(180).step()
      animationOne.translate(-50, -60).rotateZ(360).opacity(1).step()
      animationTwo.translate(-90, 0).rotateZ(360).opacity(1).step()
      animationThree.translate(-50, 60).rotateZ(360).opacity(1).step()
      this.animationMain=animationMain.export()
      this.animationOne=animationOne.export()
      this.animationTwo=animationTwo.export()
      this.animationThree=animationThree.export()
      this.hasPopped =true;

    },
    // 收回子菜单
    takeback(){
      let animationMain = wx.createAnimation({
        duration: 200,
        timingFunction: 'ease-out'
      })
      let animationOne = wx.createAnimation({
        duration: 200,
        timingFunction: 'ease-out'
      })
      let animationTwo = wx.createAnimation({
        duration: 200,
        timingFunction: 'ease-out'
      })
      let animationThree = wx.createAnimation({
        duration: 200,
        timingFunction: 'ease-out'
      })
      animationMain.rotateZ(0).step();
      animationOne.translate(0, 0).rotateZ(0).opacity(0).step()
      animationTwo.translate(0, 0).rotateZ(0).opacity(0).step()
      animationThree.translate(0, 0).rotateZ(0).opacity(0).step()
      this.animationMain=animationMain.export()
      this.animationOne=animationOne.export()
      this.animationTwo=animationTwo.export()
      this.animationThree=animationThree.export()
      this.hasPopped =false;
    },
    init(params) {
      wx.getLocation({
        success: (res) => {
          this.getWeather(`${res.latitude},${res.longitude}`)
        },
        fail: (res) => {
          this.fail(res)
        }
      })
    },
    getWeather(location){
      let that =this;
      wx.request({
        url:'https://free-api.heweather.com/s6/weather',
        data: {
          location:location,
          key,
        },
        dataType:'json',
        header: {'content-type': 'application/json'},
        success:(res)=>{
          console.log(res,'成功')
            this.cityDatas= res.data.HeWeather6[0]
            console.log(this.cityDatas,'天气信息')
        },
        fail:(err)=>{
          console.log(err,'错误')
        }
      })
    },
  },
  onShow(){
    this.initSetting();

  },
  created () {
    this.init()
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
.avatarInfo {
  display: flex;
  align-items: center;
}
.avatarInfo .avatar {
  display: block;
  overflow: hidden;
  width: 60rpx;
  height: 60rpx;
  border-radius: 50%;
}
.avatarInfo .name {
  padding: 0 20rpx;
  font-size: 30rpx;
}
.avatarInfo .downArrow {
  width: 30rpx;
  height: 30rpx;
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
.pos_icon{
  height:40px;
  width:40px;
  right:70rpx;
  bottom:150rpx; 
  position:fixed;
  z-index:2;
}
.opcition0{
  opacity:0;
}
</style>
