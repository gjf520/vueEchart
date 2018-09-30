<template>
  <div class="hello">
    <div v-for='(item,index) in data' :key='index'>
        <Columnar :list="item"></Columnar>
    </div>

    <pie :list="pie_data"></pie>
    <TransverseColumnar :list="transverse_data"></TransverseColumnar>
    <!-- <maps></maps> -->
  </div>
</template>

<script>
import EChart from 'echarts';
import Columnar from './columnar.vue';
import  Pie from './pie.vue';
import  TransverseColumnar from './transverse_columnar.vue';
// import  maps from './map.vue';
export default {
  name: 'mainContent',
    data () {
        return {
          data:{
            company:{
              xData:['感烟火灾探测器','感温火灾探测器','可燃气体探测器','手动火灾报警器','无线水压表','摄像头','用户信息传输设置'],
              yData:['20','10','15','40','10','15','30'],
              series_item_style:['#BC35F1','#FF4754'],
              yAxis_max:50
            },
            alarm:{
              xData:['感烟火灾探测器','感温火灾探测器','可燃气体探测器','手动火灾报警器','无线水压表','摄像头','用户信息传输设置'],
              yData:['20','10','15','40','10','15','30'],
              series_item_style:['#02A8FF','#0157FF'],
              yAxis_max:50
            },

            hotel:{
              xData:['感烟火灾探测器','感温火灾探测器','可燃气体探测器','手动火灾报警器','无线水压表','摄像头','用户信息传输设置'],
              yData:['200','100','150','400','100','150','300'],
              series_item_style:['#42A9F2','#02B3B3'],
              yAxis_max:500
            },
          },
          pie_data:{
            legend_data:['九小场所','服装、制鞋等生产加工企业','商场、宾馆、公共娱乐场所','化工仓储企业','高层公共建筑'],
            series_data:[
                {value:335, name:'九小场所'},
                {value:310, name:'服装、制鞋等生产加工企业'},
                {value:1548, name:'商场、宾馆、公共娱乐场所'},
                {value:135, name:'化工仓储企业'},
                {value:400, name:'高层公共建筑'}
            ]
          },
          transverse_data:{
            yData:['通源照明','源进节能科技','展高文化','米兰灯饰','山毅工程','文思海辉','企宣汇印刷','千鹤纸业','青棕成工程','汇升生物科技'],
            xData: [997, 899, 800, 732, 684, 617,519,402,330,305],
            series_item_style:['#019FFF','#0256FF'],
            xAxis_max:1000
          }
        }
    },
    components: {
      Columnar,
      Pie,
      TransverseColumnar,
      // maps
    },
    mounted() {

    },
    methods: {

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.hello{
  background-image:url(../assets/bg.png);
  height: 100%;

}
.testEcharts{
    border-right:0;
    border-left: 0;
    width:50%;
    height:300px;
    background-color: red;
}
</style>
