<template>
    <div class="content" ref="content">
        
       <ol  v-if="data.ulClass=='alignItems'"   :class="data.ulClass" ref="ul">
            <li class="blue" style="height:50px">0</li>
            <li class="blue" style="height:150px">1</li>
            <li class="blue" style="height:100px">2</li>
            <li class="blue" style="height:30px">3</li>
        </ol>

       <ol v-else  :class="data.ulClass" ref="ul">
            <li v-for="(item,idx) in liArr" :key="idx" class="blue">{{idx}}</li>
        </ol>
        <ol class="listUl">

            <!-- 单选 -->
            <li v-if="!data.isdb" v-for="item in data.radioArr" :key="item"> <el-radio v-model="radio" :label="item">{{item}}</el-radio></li>
            <!-- 多选 -->
            <li v-if="data.isdb" >
                <el-row>
                    <el-col :span="10" >
                    <el-select v-model="isdb.o1">
                    <el-option
                    v-for="item in data.radioArr[0]"
                    :key="item"
                    :label="item"
                    :value="item">
                    </el-option>
                </el-select>
                </el-col>
                <el-col :span="2" >--</el-col>
                <el-col :span="10" >
                    <el-select v-model="isdb.o2">
                    <el-option
                    v-for="item in  data.radioArr[1]"
                    :key="item"
                    :label="item"
                    :value="item">
                    </el-option>
                </el-select>
                </el-col>
                </el-row>
            </li>
           
        </ol>
        <ol class="listUl">
            <li><el-button size="small" @click='addBtn' :disabled="data.ulClass=='alignItems'">添加子元素</el-button></li>
        </ol>
        <div class="info">
            <h2>{{data.ulClass}}</h2>
            <div class="showCss">
               <el-col :span="12">
                    <pre> 
                        
        <span class="span">.{{data.ulClass}}</span>{ 

            <span class="span"> {{data.ulClass.replace(/([A-Z])/g,"-$1").toLowerCase()}}</span> : <span class="span">{{radio?radio:(isdb.o1+' '+isdb.o2)}}</span>

        }
                        
                    </pre>
               </el-col>
               <el-col :span="12">
                    <div>
                         <p v-if="data.ulClass!='flexFlow'" v-for="(item,idx) in liText" :key="idx" class="textP">
                         <span>{{item.name}}</span>:     <span>{{item.text}}</span>
                        </p>
                         <P v-if="data.ulClass=='flexFlow'">
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
            liText:[],
            text:""
        }
    },
    computed: {
       

    },
    watch: {
        // 设置flex样式
        radio(val) {
                this.$refs.ul.style[this.data.ulClass] = val;
                if(this.data.isLi) this.liStyle[this.data.liClass]=val
        },
        "isdb.o1"(val){
                this.$refs.ul.style[this.data.ulClass] = val+" "+this.isdb.o2;
            
        },
        "isdb.o2"(val){
                this.$refs.ul.style[this.data.ulClass] = this.isdb.o1+"  "+val;
            
        }
    },
    mounted () {
        this.$nextTick(()=>{
            if(!this.data.isdb) this.radio=this.data.radioArr[0]
            if(this.data.isdb) this.isdb={o1:this.data.radioArr[0][0],o2:this.data.radioArr[1][0]}
            let arr=[]
             switch (this.data.ulClass) {
            case "flexDirection":
                   arr =["默认值）主轴为水平方向，起点在左端","主轴为水平方向，起点在右端","主轴为垂直方向，起点在上沿","主轴为垂直方向，起点在下沿"]
                        this.data.radioArr.forEach((item,idx)=>{
                            this.liText.push({name:item,text:arr[idx]})
                        })
                break;
            case "flexFlow":
                  this.text="flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap"
                break;
            case "justifyContent":
                arr =["（默认值）左对齐","右对齐","居中","两端对齐，项目之间的间隔都相等","每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍"]
                        this.data.radioArr.forEach((item,idx)=>{
                            this.liText.push({name:item,text:arr[idx]})
                        })
                break;
            case "flexWrap":
                arr=["（默认）不换行","换行，第一行在上方","换行，第一行在下方"]
                this.data.radioArr.forEach((item,idx)=>{
                    this.liText.push({name:item,text:arr[idx]})
                })
                break;
            case "alignItems":
                arr=["交叉轴的起点对齐","交叉轴的终点对齐","交叉轴的中点对齐","项目的第一行文字的基线对齐","默认值,如果项目未设置高度或设为auto，将占满整个容器的高度"]
                this.data.radioArr.forEach((item,idx)=>{
                    this.liText.push({name:item,text:arr[idx]})
                })
                break;
            case "alignContent":
                arr=["与交叉轴的起点对齐","与交叉轴的终点对齐","与交叉轴的中点对齐","与交叉轴两端对齐，轴线之间的间隔平均分布","每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍","轴线占满整个交叉轴"]
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
        }
    }
}
</script>
<style lang="scss">
.content{
    position:absolute;
    left:0;
    top:0;
    width:100%;
    height:100%;
    padding:20px;
    box-sizing: border-box;
   ol .blue{
       background-color: rgb(22, 101, 153);
   }
}

/* 排列方向 flex-direction: row | row-reverse | column | column-reverse;*/
.flexDirection {  flex-direction: row;}

 /* 对齐方式 flex-wrap: nowrap | wrap | wrap-reverse;*/
.flexWrap{    flex-wrap:nowrap    }

/*flex-flow属性是flex-direction属性和flex-wrap属性的简写形式*/
.flexFlow{    flex-flow:row wrap;}

 /* 主轴上的对齐 justify-content: flex-start | flex-end | center | space-between | space-around;*/
.justifyContent{   justify-content:flex-start    }

/*在交叉轴上的对齐 align-items: flex-start | flex-end | center | baseline | stretch;*/
.alignItems{    align-items:flex-start  }

/*align-content: flex-start | flex-end | center | space-between | space-around | stretch;*/
.alignContent{       align-content: flex-start       }

//z子盒子

</style>
