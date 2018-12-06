<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <h2>Ecosystem</h2> -->
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
              // backgroundColor: "#111c4e",
              color: ['#3398DB'],
              legend: {
                  // data:['火灾数量','经济损失']，
                  data:[
                    {
                      name: '火灾数量',
                      // 强制设置图形为圆。
                      icon: 'image://../../static/logo.png',
                      textStyle: {
                          color: 'white'
                      }
                    },{
                      name: '经济损失',
                      // 强制设置图形为圆。
                      icon: 'image://../../static/logo.png',
                      textStyle: {
                          color: 'white'
                      }
                    }
                  ]

              },
              xAxis: [{
                  type: 'category',
                  gridIndex: 0,
                  data: this.list.xData,
                  axisTick: {
                      alignWithLabel: true,
                      show:false,
                  },
                  axisLine: {
                      lineStyle: {
                          color: '#0c3b71'
                      }
                  },
                  axisLabel: {
                      show: true,
                      color: 'rgb(170,170,170)',
                      fontSize: 12
                  }
              }],
              yAxis: [
                {
                      type: 'value',
                      name:'（起）',
                      nameLocation:'start',
                      nameTextStyle: {
                        color: 'rgba(255,255,255,0.7)',
                        fontSize: 12,
                        padding: [-21,60,0,0]
                        // padding: [0,0,30,0]
                      },
                      max:5,
                      gridIndex: 0,
                      splitLine: {
                          show: false
                      },
                      axisTick: {
                          show: true,
                      },
                      axisLine: {
                          show:true,
                          lineStyle: {
                              color: '#979797'
                          }
                      },
                      axisLabel: {
                          color: 'rgb(170,170,170)',
                          formatter: '{value}'
                      }
                  },
                  {
                      type: 'value',
                      name:'（万元）',
                      nameLocation:'start',
                      nameTextStyle: {
                        color: 'rgba(255,255,255,0.7)',
                        fontSize: 11.33,
                        fontSize: 12,
                        padding: [-21,0,0,70]
                      },
                      max:5,

                      // splitLine: {
                      //     show: false
                      // },
                      // axisLine: {
                      //     show: true
                      // },
                      // axisTick: {
                      //     show: false
                      // },
                      // axisLabel: {
                      //     show: false
                      // },
                      gridIndex: 0,
                      splitLine: {
                          show: false
                      },
                      axisTick: {
                          show: true
                      },
                      axisLine: {
                          show:true,
                          lineStyle: {
                              color: '#979797'
                          }
                      },
                      axisLabel: {
                          color: 'rgb(170,170,170)',
                          formatter: '{value}'
                      }
                  }
                ],
                series: [{
                        name: '火灾数量',
                        type: 'bar',
                        barWidth: '20',
                        xAxisIndex: 0,
                        yAxisIndex: 0,
                        itemStyle: {
                            normal: {
                                color:  new EChart.graphic.LinearGradient(
                                    0, 0, 0, 1, [{
                                            offset: 0,
                                            color: '#ed4451'
                                        },
                                        {
                                            offset: 0.5,
                                            color: '#612e43'
                                        },
                                        {
                                            offset: 1,
                                            color: '#1b213b'
                                        }
                                    ]
                                )
                            }
                        },

                        data: this.list.yData,
                        zlevel: 11

                    },
                    {
                        name: '背景',
                        type: 'bar',
                        // barWidth: '30%',
                        // barGap:'-100%',
                        barWidth: 20,
                        silent:true,
                        barGap:'-100%',
                        xAxisIndex: 0,
                        yAxisIndex: 1,
                        data: [5, 5, 5, 5, 5],
                        itemStyle: {
                            normal: {
                                color: 'rgba(255,255,255,0.1)'
                            }
                        },
                        zlevel: 9
                    },{
                        name: '经济损失',
                        type: 'line',
                        symbolSize:10,  //拐点圆的大小
                        // symbol: ' ',   //设置拐点的样式，可以设置图案，只需写图案的路径就好
                        barWidth: 20,
                        silent:true,
                        barGap:'-100%',
                        data: ['3','2','4','1','5'],
                        itemStyle: {
                            normal: {
                                color: 'rgba(255,255,255,0.1)',
                                lineStyle:{
                                  color:'#14e6c6'
                                }
                            }
                        },
                        zlevel: 11
                    },

                ]
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
    width:520px;
    height:300px;
    /* background-color: red; */
}
</style>
