<template>
  <div class="hello">
    <gradientLine></gradientLine>
    <moreBar></moreBar>
    <pieRisk :list="pie_data"></pieRisk>
     <div v-for='(item,index) in data' :key='index'>
        <Columnar :list="item"></Columnar>
    </div>
      <pie :list="pie_data"></pie>
     <zhexian :list='company'></zhexian>
     <pieRisk :list="pie_data"></pieRisk>
     <noticeColumnar></noticeColumnar>
     <div class='prcentBar'>
       <div class='progress' v-for='(item,index) in companyname' :key='index'>
         <progressImg  :stepValue="0.1" :initValue="1" :stopValue='item.percent' :name='item.name'></progressImg>
       </div>
     </div>
     <bar :list='company'></bar>



    <TransverseColumnar :list="transverse_data"></TransverseColumnar>

    <maps></maps>
    <pieColor></pieColor>

    <!--  -->
  </div>
</template>

<script>
import EChart from 'echarts';
import Columnar from './columnar.vue';
import gradientLine from './gradient_line_chart';
import  Pie from './pie.vue';
import  bar from './bar.vue';
import moreBar from './more_bar.vue'
import  TransverseColumnar from './transverse_columnar.vue';
import  maps from './map.vue';
import  zhexian from './zhexian.vue';
import  pieRisk from './pie_risk.vue';
import  noticeColumnar from './notice_columnar.vue';
import  progressImg from './progress.vue';




export default {
  name: 'mainContent',
    data () {
        return {
          companyname:['召陵人民医院', '召陵人民医院', '新城区人民医院', '新城区中医院', '民政康复医院'],
          companyname:[
            {
              name:'召陵人民医院',
              percent:40
            },{
              name:'召陵人民医院',
              percent:50
            },{
              name:'新城区人民医院',
              percent:66
            },{
              name:'新城区中医院',
              percent:33
            },{
              name:'民政康复医院',
              percent:77
            }
          ],

          company:{
            xData:['单层','多层','高层','地下','是有化工企业'],
            yData:['1','3','4','2','4'],
            series_item_style:['#BC35F1','#FF4754'],
            yAxis_max:5
          },
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
            legend_data:['住宅','人员密集场所','交通工具','垃圾及废弃物','农副业场所','物资仓储场所','其他'],
            series_data:[
                {value:335, name:'住宅'},
                {value:310, name:'人员密集场所'},
                {value:1548, name:'交通工具'},
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
      gradientLine,
      moreBar,
      Pie,
      bar,
      TransverseColumnar,
      maps,
      zhexian,
      pieRisk,
      noticeColumnar,
      progressImg
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
.prcentBar{
  margin-right: 1700px;
}
.progress{
  position: relative;
  width: 350px;
  height: 10px;
  left: 70%;
  top: 40%;
  margin-bottom: 30px;
  border:1px solid #263747;
  background-color: rgba(87,88,88,0.4);
}
.title{
  color: white;
  font-size: 16px;

}


</style>
