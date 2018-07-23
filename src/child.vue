<template>
    <div  class="swiper-container">
    <div class="swiper-wrapper">
        <div class="swiper-slide">
          <child :data="componentData.order"/>
        </div>
        <div class="swiper-slide">
          <child :data="componentData.flexGrow"/>
        </div>
        <div class="swiper-slide">
          <child :data="componentData.flexShrink"/>
        </div>
        <div class="swiper-slide">
          <child :data="componentData.alignSelf"/>
        </div>
        
        
       
      
      </div>
       <!-- 如果需要滚动条 -->
    <div class="swiper-scrollbar"></div>
  </div>
   
</template>

<script>
import child from './components/child'
import Swiper from 'swiper'
export default {
  components:{child},
  data () {
    return {
     componentData:{
      order:{
        liClass:"order",
         radioArr:[ "1" , "10" , "20" , "30" , "40" , "50"]
      },
      flexGrow:{
        liClass:"flexGrow",
         radioArr:[ "1" , "5" , "10" , "15" , "20" , "25"]
      },
      flexShrink:{
        liClass:"flexShrink",
         radioArr:[ "1" , "5" , "10" , "15" , "20" , "25"]
      },
      alignSelf:{
        liClass:"alignSelf",
         radioArr:[ "auto" , "flex-start" , "flex-end" , "center" , "baseline" , "stretch"]
      },
     }

    }
  },
  mounted () {
   this.$nextTick(()=>{
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
