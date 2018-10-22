<template>
  <div class="container">
    <image class='bcg' src="/static/fog-himalayas-landscape-38326.jpg" mode='aspectFill'/>
    <div class="sear">
      <img src="../../img/search.png"/>
      <input class="input_sty" placeholder="查询其他城市天气" v-model="searchVal"/>
    </div>
    <!-- 主体部分 -->
    <div class="content">
      <div>头像 - 用户名</div>
      <div style="display:flex;justify-content:space-between;">
        <span style="font-size:62rpx;">{{cityDatas.basic.location || '定位中'}}</span>
        <span style="font-size:22rpx">{{cityDatas.updateTimeFormat}}更新</span>
      </div>
      <div style="font-size:22rpx; margin-top:30rpx;">
        下午好，长时间敲代码，能让你的腰间盘更加突出噢
      </div>
      <div class="weather_info">
        <div class="temp">{{cityDatas.now.tmp || '-'}}</div>
        <div class="weather">{{cityDatas.now.cond_txt || '--'}}℃</div>
        <span class="pm">能见度 {{cityDatas.now.vis}}</span>
      </div>
      <div class="guide">
        <div class="item" v-for="(item,index) in cityDatas.daily_forecast" :key="index">
          <div>{{item.date}}</div>
          <div>{{item.tmp_min}}~{{item.tmp_max}}°</div>
          <div>{{item.cond_txt_d}}</div>
          <div>{{item.wind_dir}}</div>
        </div>
      </div>
      <div class="livingIndex">
        <div class="item" v-for="(item,index) in cityDatas.lifestyle" :key="index" v-bind:style="{ 'border': index+1==5 ? '0':''}">
          <img src='/img/lifestyle_{{item.type}}.png' class="icon"/>
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
      <img src="/static/location.png" :animation="animationOne"  bindtap="menuOne" class="pos_icon opcition0"/>
      <img src="/static/setting.png" :animation="animationTwo" bindtap="menuTwo" class="pos_icon opcition0"/>
      <img src="/static/info.png" :animation="animationThree" bindtap="menuThree" class="pos_icon opcition0"/>
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
          console.log(`${res.latitude},${res.longitude}`,'lad')
          this.getWeather(`${res.latitude},${res.longitude}`)
        },
        fail: (res) => {
          this.fail(res)
        }
      })
    },
    getWeather(location){
      let that =this;
      // wx.request({
      //   url:'https://free-api.heweather.com/s6/weather',
      //   data: {
      //     location:location,
      //     key,
      //   },
      //   dataType:'json',
      //   header: {'content-type': 'application/json'},
      //   success:(res)=>{
      //     console.log(res,'成功')
      //       this.cityDatas= res.data.HeWeather6[0]
      //       console.log(this.cityDatas,'天气信息')
      //   },
      //   fail:(err)=>{
      //     console.log(err,'错误')
      //   }
      // })
      let data = {"HeWeather6":[{"basic":{"cid":"CN101021600","location":"虹口","parent_city":"上海","admin_area":"上海","cnty":"中国","lat":"31.26096916","lon":"121.49182892","tz":"+8.00"},"update":{"loc":"2018-10-22 11:46","utc":"2018-10-22 03:46"},"status":"ok","now":{"cloud":"75","cond_code":"305","cond_txt":"小雨","fl":"19","hum":"98","pcpn":"2.2","pres":"1019","tmp":"17","vis":"6","wind_deg":"57","wind_dir":"东北风","wind_sc":"0","wind_spd":"1"},"daily_forecast":[{"cond_code_d":"305","cond_code_n":"101","cond_txt_d":"小雨","cond_txt_n":"多云","date":"2018-10-22","hum":"84","mr":"16:09","ms":"03:22","pcpn":"1.0","pop":"55","pres":"1019","sr":"06:02","ss":"17:13","tmp_max":"19","tmp_min":"16","uv_index":"1","vis":"14","wind_deg":"355","wind_dir":"北风","wind_sc":"1-2","wind_spd":"6"},{"cond_code_d":"101","cond_code_n":"100","cond_txt_d":"多云","cond_txt_n":"晴","date":"2018-10-23","hum":"65","mr":"16:42","ms":"04:17","pcpn":"1.0","pop":"55","pres":"1021","sr":"06:03","ss":"17:12","tmp_max":"23","tmp_min":"15","uv_index":"4","vis":"18","wind_deg":"181","wind_dir":"南风","wind_sc":"1-2","wind_spd":"11"},{"cond_code_d":"101","cond_code_n":"101","cond_txt_d":"多云","cond_txt_n":"多云","date":"2018-10-24","hum":"63","mr":"17:17","ms":"05:15","pcpn":"0.0","pop":"1","pres":"1022","sr":"06:04","ss":"17:11","tmp_max":"24","tmp_min":"14","uv_index":"3","vis":"20","wind_deg":"93","wind_dir":"东风","wind_sc":"1-2","wind_spd":"11"}],"lifestyle":[{"type":"comf","brf":"舒适","txt":"白天不太热也不太冷，风力不大，相信您在这样的天气条件下，应会感到比较清爽和舒适。"},{"type":"drsg","brf":"较舒适","txt":"建议着薄外套、开衫牛仔衫裤等服装。年老体弱者应适当添加衣物，宜着夹克衫、薄毛衣等。"},{"type":"flu","brf":"易发","txt":"天冷空气湿度大，易发生感冒，请注意适当增加衣服，加强自我防护避免感冒。"},{"type":"sport","brf":"较不宜","txt":"有降水，推荐您在室内进行健身休闲运动；若坚持户外运动，须注意携带雨具并注意避雨防滑。"},{"type":"trav","brf":"适宜","txt":"温度适宜，又有较弱降水和微风作伴，会给您的旅行带来意想不到的景象，适宜旅游，可不要错过机会呦！"},{"type":"uv","brf":"最弱","txt":"属弱紫外线辐射天气，无需特别防护。若长期在户外，建议涂擦SPF在8-12之间的防晒护肤品。"},{"type":"cw","brf":"不宜","txt":"不宜洗车，未来24小时内有雨，如果在此期间洗车，雨水和路上的泥水可能会再次弄脏您的爱车。"},{"type":"air","brf":"良","txt":"气象条件有利于空气污染物稀释、扩散和清除，可在室外正常活动。"}]}]}
      this.cityDatas= data.HeWeather6[0]
    },
  },
  created () {
    // this.init()
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
