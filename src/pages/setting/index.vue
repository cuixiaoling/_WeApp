<template>
  <div class="wrap">
        <div class="unit">
          <div class="title">
            自定义
          </div>
          <div class="content">
            <div>打开顶部城市天气快捷搜索</div>
            <switch color='#40a7e7' bindchange='switchChange' data-switchparam='hiddenSearch'></switch>
          </div>
          <div class="content">
            <div>显示生活指数信息</div>
            <switch color='#40a7e7' bindchange='switchChange' data-switchparam='hiddenSearch'></switch>
          </div>
        </div>
        <div class="unit">
          <div class="title">检测更新</div>
          <div class="content">
            <div class="tip">
              <div>打开首页更新信息</div>
              <div style="font-size:22rpx;color:#999;">在首页检测到新版本，会提示更新</div>
            </div>
            <switch color='#40a7e7' bindchange='switchChange' data-switchparam='hiddenSearch'></switch>
          </div>
      </div>
      <div class="unit">
        <div class="title">小工具</div>
        <div style="color:#40a7e7;font-size:28rpx;">NFC</div>
        <div class="content pl20">
          <div>检测是否支持NFC</div>
          <img src="/static/arrow.png" alt="" class="more">
        </div>
        <div style="color:#40a7e7;font-size:28rpx;">屏幕亮度</div>
        <div class="content pl20">
          <div class="tip">
            <div>当前亮度</div>
            <div style="font-size:22rpx;color:#999;">范围0~100，0最暗，100最亮</div>
          </div>
          <div>50</div>
        </div>
        <div class="content pl20">
          <div style="width:100%">
            <div>设置屏幕亮度</div>
            <slider min='0' max='100' step='1' block-size='12' block-color='#40a7e7' activeColor='#40a7e7' show-value='true' bindchange='screenBrightnessChanging' bindchanging='screenBrightnessChanging'></slider>
          </div>
        </div>
        <div class="content pl20">
            <div class="tip">
              <div>保持亮度</div>
              <div style="font-size:22rpx;color:#999;">仅在当前小程序、当次生效、离开小程序后设置失效</div>
            </div>
            <switch color='#40a7e7' bindchange='switchChange' data-switchparam='hiddenSearch'></switch>
          </div>
        <div style="color:#40a7e7;font-size:28rpx;">系统信息</div>
        <div class="content">
          <div>查看系统信息</div>
          <img src="/static/arrow.png" alt="" class="more">
        </div>
      </div>
      <div class="unit">
        <div class="title">清除数据</div>
        <div class="content">
          <div class="tip">
            <div>首页悬浮球复位</div>
            <div style="font-size:22rpx;color:#999;">首页悬浮球将复位到右下角</div>
          </div>
         <img src="/static/arrow.png" alt="" class="more">
        </div>
        <div class="content">
          <div class="tip">
            <div>恢复初始化设置</div>
            <div style="font-size:22rpx;color:#999;">所有设置信息都将被清除</div>
          </div>
         <img src="/static/arrow.png" alt="" class="more">
        </div>
        <div class="content">
          <div class="tip">
            <div>清除所有本地数据</div>
            <div style="font-size:22rpx;color:#999;">所有本地数据都将被清除</div>
          </div>
         <img src="/static/arrow.png" alt="" class="more">
        </div>
      </div>
  </div>

</template>
<script>
export default {
  methods:{
    initFun(){
      wx.setNavigationBarTitle({
      title: '设置'
    })
    }
  },
  mounted(){
    this.initFun();
  }
}
</script>
<style>
.wrap{
  font-size: 28rpx;
  color:#666;
}
.unit{ 
  padding: 0 40rpx;
  background:#fff;
  margin-bottom:20rpx;
}
.title{
  color:#40a7e7;
  font-size:32rpx;
  padding:26rpx 0;
}
.content{
  display: flex;
  justify-content:space-between;
  height: 100rpx;
  align-items: center;
}
.tip{
  display:flex; 
  flex-direction: column;
}
.more{
  width: 32rpx;
  height: 32rpx;
}
slider{
  margin: 0;
}
.pl20{
  padding-left: 20rpx;
}
</style>

