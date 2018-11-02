<template>
  <div class="warp">
    <div class="search">
    <img class="icon" src="../../img/search.png">
      <input type="text" class="sear_input" placeholder="搜索城市">  
      <div style="color:#666;">清空</div>
    </div>
    <!-- <div class="content" v-for="(item,index) in cityList" :key="index">
      <div class="key">{{item[0]}}</div>
      <div class="value" v-for="(item2,index2) in item[1]" :key="index2">
        {{item2}}
      </div>
    </div> -->
    <div class="content" v-for="(item,index) in showItems" :key="index">
      <div class="key">{{index}}</div>
      <div class="value" v-for="(item2,index2) in item" :key="index2">
        {{item2.name}}
      </div>
    </div>
  </div>
</template>

<script>
import staticData  from '../../data/staticData.js'
export default {
  data(){
    return{
      // cityList:[
      //   ['A',[1,2,3]],
      //   ['b',[1,2,3]],
      //   ['c',[1,2,3]],
      //   ['d',[1,2,3]],
      // ],
      cityList:[],
      showItems:[],
      
    }
  },
  methods: {
    initFun(){
      wx.setNavigationBarTitle({
        title:'选择城市'
      })
    },
    // 按照字母顺序生成需要的数据格式
    getAreaObj(){
      let areas = staticData.cities
      // 比较大小
      areas = areas.sort((a,b)=>{
        if(a.letter >b.letter){
          return 1
        }
        if(a.letter < b.letter){
          return -1
        }
        return 0;
      })
      // console.log(areas,'aaaaaaaaa')
      let obj = {}
      for(let i=0,len=areas.length;i<len;i++){
        let item=areas[i];
        delete item.districts
        let letter = item.letter;
        if(!obj[letter]){
          obj[letter]=[]
        }
        // console.log(obj[letter],'2222')
        obj[letter].push(item);
        // console.log(obj[letter].push(item),'11111')

      }
      return obj;
    },
    getPost(){
      console.log(staticData.cities,'数据');
      let cityArr=staticData.cities
      let arr0 = ['A','B','C','D','E','F','G','H','L','M','N','O','P','Q','R','S','T','U','V','W','S','Y','Z'];
      let arr = [];
      for(let i=0;i<arr0.length;i++){
        let arr1=arr0[i];
        let arrItem=[];
        let arr2=[];
        for(let j =0;j<cityArr.length;j++){
          if(arr0[i]==cityArr[j].letter){
            arrItem.push(cityArr[j].name);
          }
        }
        if(arrItem.length!=0){
          arr2.push(arr1,arrItem)
          arr.push(arr2)
        }
      }
      console.log(arr,'arrarrarr');
      this.cityList= arr;
    },
  },
  mounted(){
    this.initFun();
    this.getPost();
    let arr = this.getAreaObj();
    this.showItems=arr
    console.log(arr,'aaaaa')
  }
}
</script>

<style>
.search{
  font-size: 30rpx;
  background: #fff;
  padding:30rpx;
  position: fixed;
  position: relative;
  display: flex;
  width:100%;
}
.icon{
  width:28rpx;
  height:28rpx;
  margin-right:10rpx;

}
.sear_input{
  border: 1rpx solid #fff;
  background:#f4f6f9;
  width: 80%;
}
.content{
  font-size: 32rpx;
}
.key{
  background:#f4f6f9;
  height:50rpx;
  display:flex;
  align-items:center;
  padding:0 30rpx;
}
.value{
  border-bottom:1rpx solid #efefef;
  height:104rpx;
  display:flex;
  align-items:center;
  padding:0 30rpx;
  background:#fff;
}
</style>
