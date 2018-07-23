<template>
    <div class="test">
        <ul ref="ul"> 
            <li :a="a"></li>
            <el-button @click="jia"></el-button>
        </ul> 
    </div>
</template>
<script>
import {mixinTest1} from '../mixins/index.js';
    export default{
        mixins:[mixinTest1],
        data(){
            return {
                a:33
            }
        },
        created(){
        },
        methods:{
            jia(){
                this.a++
            }
        },
        mounted () {
        },
        filters:{
            fil(val){
               return this.a*1000
            }
        },
        directives:{
            color:{
                inserted(el,bind){
                    console.log(el)
                }
            }
        }
    }
</script>
<style lang="scss">
.test{
  
}
</style>

