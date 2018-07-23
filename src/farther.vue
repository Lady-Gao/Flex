<template>
    <div  class="swiper-container">
    <div class="swiper-wrapper">
        <div class="swiper-slide">
          <flexDome :data="componentData.flexDirection"/>
        </div>
        <div class="swiper-slide">
          <flexDome :data="componentData.flexWrap"/>
        </div>
        <div class="swiper-slide">
          <flexDome :data="componentData.flexFlow"/>
        </div>
        <div class="swiper-slide">
          <flexDome :data="componentData.justifyContent"/>
        </div>
        <div class="swiper-slide">
          <flexDome :data="componentData.alignItems"/>
        </div>
        <div class="swiper-slide">
          <flexDome :data="componentData.alignContent"/>
        </div>
       
      
      </div>
       <!-- 如果需要滚动条 -->
    <div class="swiper-scrollbar"></div>
  </div>
   
</template>

<script>
import flexDome from './components/flexDome'
import Swiper from 'swiper'
export default {
  components:{flexDome},
  data () {
    return {
     componentData:{
      flexDirection:{
        ulClass:"flexDirection",
        liColor:"red",
        radioArr:["row" , "row-reverse" , "column" , "column-reverse"]
      },
      flexFlow:{
        isdb:true,
        ulClass:"flexFlow",
        liColor:"red",
        radioArr:[["row" , "row-reverse" , "column" , "column-reverse"],['nowrap' , 'wrap' , 'wrap-reverse']]
      },
      justifyContent:{
        ulClass:"justifyContent",
        liColor:"green",
        radioArr:["flex-start" ,"flex-end" , "center" , "space-between" , "space-around"]
      },
      flexWrap:{
        ulClass:"flexWrap",
        liColor:"green",
        radioArr:['nowrap' , 'wrap' , 'wrap-reverse']
      },
      alignItems:{
        ulClass:"alignItems",
        liColor:"bule",
        radioArr:["flex-start" , "flex-end" , "center" , "baseline" , "stretch"]
      },
      alignContent:{
        ulClass:"alignContent",
        liColor:"bule",
        radioArr:["flex-start" , "flex-end" , "center" , "space-between" , "space-around" , "stretch"],      },
     }

    }
  },
  mounted () {
   this.$nextTick(()=>{
     //组件绑定index做滚滚屏
   
        var mySwiper = new Swiper ('.swiper-container', {
          speed:500,							//滑动的速度 
          
          grabCursor : true,
          autoplayDisableOnInteraction: false,
          observer:true, //修改swiper自己或子元素时，自动初始化swiper
          observeParents:true,//修改swiper的父元素时，自动初始化swiper
          scrollbar: {
            el: '.swiper-scrollbar',
          },
     })
   })
  }
}
</script>

<style lang="scss">

.swiper-container {
    width: 100%;
    height: 100%;
}
</style>
