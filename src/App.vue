<template>
    <div id="app" >
    <farther/>
    <child/>
    <!-- <test/>> -->
  </div>
   
</template>

<script>
import farther from './farther'
import child from './child'
import test from './test/test'
export default {
  components:{farther,child,test},
  name: 'app',
  data () {
    return {
    }
  }
}
</script>

<style lang="scss">
#app{
  position:absolute;
  width:100%;
  height:100%
}

</style>
