<template>
  <div class="hello">
    <div class="testEcharts" ref="statistics"></div>
  </div>
</template>

<script>
import EChart from 'echarts'

export default {
    props:{
        list:{
            type:Object,
            default:()=>{}
        }
    },
    data () {
        return {
          statistics:{
              option: {},
              chart: {},
              element: {},
          },
        }
    },
    mounted() {
       this.initData();
       window.onresize = ()=>{
         this.statistics.chart.resize();
       }
    },
    destory(){
        window.onresize = null;
    },
    methods: {
        initData(){
            this.statistics.option = {
              // backgroundColor: '#00265f',

               tooltip: {
                   trigger: 'axis',
                   axisPointer: {
                       lineStyle: {
                           color: '#57617B'
                       }
                   }
               },
               grid: {
                   left: '3%',
                   right: '4%',
                   bottom: '3%',
                   containLabel: true
               },
               xAxis: [{
                   type: 'category',
                   boundaryGap: true,  //X轴不从0刻度开始
                   // x轴的字体样式
                   axisLabel: {
                        show: true,
                        textStyle: {
                            color: '#979797',
                            fontSize:'12'
                        },
                        formatter: function(value, index){
                          var val_arr = value.split('-');
                          var str = `${val_arr[0]}\n{b||}\n${val_arr[1]}`;
                          return str;
                        },
                        rich: {
                          b: {
                            fontSize: 10,
                            lineHeight: 12
                          }
                        },
                    },
                    // 是否显示坐标刻度
                    axisTick: {
                        show: false,
                    },
                   axisLine: {
                       lineStyle: {
                           color: '#0d5672'
                       }
                   },

                   data: ['0:00-2:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00', '2:00-4:00']
               }],
               yAxis: [{
                   name:'（个）',
                   nameTextStyle: {
                     fontSize: 14,
                     padding: [-21, 20, 0, 0]
                   },
                   type: 'value',
                   // 是否显示坐标刻度
                   axisTick: {
                       show: true
                   },
                   axisLine: {
                     lineStyle: {
                         color: '#979797'
                     }
                   },
                   axisLabel: {
                       margin: 10,
                       textStyle: {
                           fontSize: 14
                       }
                   },
                   splitLine:{
                     show:true,
                     interval:1,
                     lineStyle:{
                       color:"#0c3347",
                     }
                   },
                   splitArea:{
                     show:true,
                     interval:2,
                     areaStyle:{
                       color: ['#0e1d31','#061219'] ,
                       shadowColor: '#0e1d31',
                       shadowBlur: 2
                     }
                   }
               }],
               series: [{
                   // name: '',
                   type: 'line',
                   smooth: true,
                   symbol: 'circle',
                   symbolSize: 5,
                   showSymbol: false,
                   lineStyle: {
                       normal: {
                           width: 1
                       }
                   },
                   // areaStyle: {
                   //     normal: {
                   //         color: new EChart.graphic.LinearGradient(0, 0, 0, 1, [{
                   //             offset: 0,
                   //             color: '#b833e8'
                   //         }, {
                   //             offset: 0.8,
                   //             color: '#62298c'
                   //         }], false),
                   //         shadowColor: 'rgba(0, 0, 0, 0.1)',
                   //         shadowBlur: 10
                   //     }
                   // },
                   itemStyle: {
                       normal: {
                           color: 'rgb(80,37,211)',
                           borderColor: 'rgba(112,43,154,0.27)',
                           borderWidth: 12

                       }
                   },
                   data: [0, 60, 191, 134, 150, 120, 110, 125, 145, 122, 165, 122, 89, 112, 0]
               }]
            };
            this.statistics.chart = EChart.init(this.$refs.statistics)
            this.statistics.chart.setOption(this.statistics.option)
        },
    }
}
</script>
<style scoped>
.testEcharts{
    border-right:0;
    border-left: 0;
    width:50%;
    height:300px;
    /* background-color: red; */
}
</style>
