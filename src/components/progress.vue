
<template>
    <div class="processBarBox">
      <div class='title'>

        <span class="name">{{name}}</span>
        <span class="precent">{{this.toDecimal2(processValue)}}</span>
      </div>

        <transition name="fade">
            <div class="progressBar"></div>
        </transition>
    </div>
</template>
<script>
export default {
    data() {
        return {
            processValue: 0, // 进度
        }
    },
    props: {
        //自增幅度
        stepValue: {
            type: Number,
            default: 1,
        },
        //初始值
        initValue: {
            type: Number,
            default: 0,
        },
        //进度停止点
        stopValue: {
            type: Number,
            default: 100,
        },
        //单位名称
        name:{
            type: String,
            default: '',
        }
    },
    mounted() {
        this.loadProcess();
    },
    methods:{
        loadProcess(){
            this.processValue = this.initValue;
            let step =  this.stepValue;
            let timer = setInterval(() => {
                this.processValue = this.processValue + step;
                this.$el.style.width = this.processValue + '%';
                if (this.processValue >= this.stopValue) {
                    clearInterval(timer);
                    return;
                }
            },1)
        },
        toDecimal2(_value){
            var _value=Math.round(parseFloat(_value)*100)/100;
            var arr=_value.toString().split(".");
            if(arr.length==1){
                _value=arr.toString()+".00";
                return _value;
            }
            if(arr.length>1){
                if(arr[1].length<2){
                    _value=arr.toString()+"0";
                }
                return _value.replace(/\,/g,'.');
            }
        },
    },
}
</script>
<style lang="less">
    .progressBar {
        position :relative;
        top: 0px;
        height: 10px;
        width : 100%;
        /* border-radius: 20px; */
        background: linear-gradient(to right, #122a40 , #0292f4);
        transition: background-color .5s;
    }
    .fade {
            &-enter-active, &-leave-active {
            transition: all .5s;
        }
        &-enter, &-leave-active {
            opacity: 0;
        }
    }
    .title{
      position: absolute;
      top: -23px;
      width: 350px;
      display: flex;
      justify-content: space-between;
      .name{
        color:white;
        font-size: 14px;
      }
      .precent{
        color:#038ae7;
        font-size: 12px;
      }

    }
</style>
