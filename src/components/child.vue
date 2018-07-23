<template>
    <div class="content1" ref="content">
        
       <ol  ref="ul">
            <li :class="data.liClass" v-for="(item,idx) in liArr" :key="idx" @click="changeLi(idx)"  @mouseenter="mouseenter(idx)" @mouseout="mouseout(idx)">{{idx}}
            </li>
        </ol>
        <ol class="listUl">
            <li v-if="!data.isdb" v-for="item in data.radioArr" :key="item"> <el-radio v-model="radio" :label="item">{{item}}</el-radio></li>
        </ol>
        <ol class="listUl">
            <li><el-button size="small" @click='addBtn'>添加子元素</el-button></li>
        </ol>
        <div class="info">
            <h2>{{data.liClass}}</h2>
            <div class="showCss">
               <el-col :span="12">
                    <pre>
                
        <span class="span">.{{data.liClass}}{{nodeIdx}}</span>{ 

            <span class="span"> {{data.liClass.replace(/([A-Z])/g,"-$1").toLowerCase()}}</span> : <span class="span">{{radio}}</span>

        }
                        
                    </pre>
               </el-col>
               <el-col :span="12">
                    <div>
                        <p v-if="data.liClass=='alignSelf'" v-for="(item,idx) in liText" :key="idx" class="textP">
                         <span>{{item.name}}</span>:     <span>{{item.text}}</span>
                        </p>
                        <P v-if="data.liClass!='alignSelf'">
                            <span>{{text}}</span>
                            </P>
                    </div>
               </el-col>
            </div>
            </div>
    </div>
</template>
<script>
export default{
    props: ["data"],
    data(){
        return{
            radio:"",
            liArr:["li","li","li"],
            isdb:{o1:"",o2:""},
            nodeIdx:0,
            liText:[],
            text:""
        }
    },
    computed: {
       

    },
    watch: {
        // 设置flex样式
        radio(val) {
             this.$refs.ul.children[this.nodeIdx].style[this.data.liClass] = val;
        }
        },
    mounted () {
        this.$nextTick(()=>{
        this.radio=this.data.radioArr[0]
        switch (this.data.liClass) {
            case "order":
                 this.text="排列顺序。数值越小，排列越靠前，默认为0"              
                break;
            case "flexGrow":
                this.text="当有多个li时，会等分剩余空间,默认为1,数值越大空间越大"
                break;
            case "flexShrink":
                this.text=`当有多个li占满父盒子宽度时;会缩小比例，默认为1，数值越大空间越小`
                break;
            case "alignSelf":
            let arr=["继承父元素的align-items属性","交叉轴的起点对齐","交叉轴的终点对齐","交叉轴的中点对齐","项目的第一行文字的基线对齐","默认值,如果项目未设置高度或设为auto，将占满整个容器的高度"]
                this.data.radioArr.forEach((item,idx)=>{
                    this.liText.push({name:item,text:arr[idx]})
                })
                break;
           
        }
        
    })
    },
    methods: {
        addBtn(){
            this.liArr.push('li')
        },
        changeLi(idx){
            this.nodeIdx=idx
            this.$refs.ul.children[this.nodeIdx].style[this.data.liClass]=this.radio
        },
        mouseenter(idx){
                 this.$refs.ul.children[idx].style.backgroundColor="red"
                 this.$refs.ul.children[idx].title="点击选中我"
        },
        mouseout(idx){
                this.$refs.ul.children[idx].style.backgroundColor="#eca408"   
        }
    }
}
</script>
<style lang="scss">
.content1{
    position:absolute;
    left:0;
    top:0;
    width:100%;
    height:100%;
    padding:20px;
    box-sizing: border-box;
    ol:nth-child(1){
       li{
            background-color: #eca408;
        }
     }   
  
}

/*排列顺序。数值越小，排列越靠前，默认为0  order:0;*/
.order{  order: 2;    }

/*单个项目有与其他项目不一样的对齐方式,可覆盖align-items属性 除了auto，其他都与align-items属性完全一致 align-self: auto | flex-start | flex-end | center | baseline | stretch;*/
.alignSelf{   align-self: auto;  }

/*属性都为1，则它们将等分剩余空间 flex-grow: 1;*/
.flexGrow{   flex-grow: 1;  }

/*缩小比例，默认为1，即如果空间不足，该项目将缩小flex-shrink: 1;*/
.flexShrink{   flex-shrink: 1;  }

</style>
