<script>
export default {
  created () {
    // 调用API从本地缓存中获取数据
    const logs = wx.getStorageSync('logs') || []
    logs.unshift(Date.now())
    wx.setStorageSync('logs', logs)

    console.log('app created and cache logs by setStorageSync')
  }
}
</script>

<style>
page{
  background:#f4f6f9;
  -webkit-user-select:none;
  user-select:none;
  width:100%;
  overflow-x:hidden;
  height:100%;
}
/* this rule will be remove */
* {
  margin:0;
}
</style>
