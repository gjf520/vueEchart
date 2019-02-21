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
                   title: {
                      text: '近一个月火警预警数TOP10联网单位',
                      textStyle: {
                        fontSize: 14,
                        color: "#EDF2F5",
                        fontStyle: "normal", //主标题文字字体风格，默认normal，有italic(斜体),oblique(斜体)
                        fontWeight: "lighter", //可选normal(正常)，bold(加粗)，bolder(加粗)，lighter(变细)，100|200|300|400|500...
                        fontFamily: "PingFangSC-Regular" //主题文字字体，默认微软雅黑
                      },
                      left: "12px",
                      top: "10px"
                    },
                   tooltip: {
                       trigger: 'axis',
                       axisPointer: {
                           type: 'shadow'
                       }
                   },
                   legend: {
                       // data: ['2011年', '2012年']
                   },
                   grid: {
                       left: '3%',
                       right: '4%',
                       bottom: '3%',
                       containLabel: true
                   },
                   xAxis: {
                       type: 'value',
                       // max: this.list.xAxis_max,
                       //
                       axisLabel: {
                          color: "#fff",

                        },
                        axisLine: {//坐标线
                            lineStyle: {
                                type: 'solid',
                                color: '#2858C6',//轴线的颜色
                                width:'1'//坐标线的宽度
                            }
                        },
                        splitLine: {
                          lineStyle: {
                              // 使用深浅的间隔色
                              type:'dashed',
                              color: 'rgba(56, 144, 254, 0.5)',
                              width:'1'//坐标线的宽度
                          }
                        },
                       boundaryGap: [0, 0.01]
                   },
                   yAxis: {
                       type: 'category',
                       axisLabel: {
                          color: "#fff",

                        },

                       data:this.list.yData
                   },
                 series: [
                     {
                         name: '2011年',
                         type: 'bar',
                         barWidth : 20,
                         itemStyle: {
                             normal: {
                                 // barBorderRadius:[0, 20, 20, 0],
                                 color: {
                                    type: 'linear',
                                    x: 0,
                                    y: 0,
                                    x2: 0,
                                    y2: 1,
                                    colorStops: [{
                                        offset: 0, color: this.list.series_item_style[0] // 0% 处的颜色
                                    }, {
                                        offset: 1, color: this.list.series_item_style[1] // 100% 处的颜色
                                    }],
                                    globalCoord: false, // 缺省为 false
                                 },//设置柱子颜色
                                 label: {
                                     show: true,//柱子上显示值
                                     position: 'right',//值在柱子上方显示
                                     textStyle: {
                                         color: '#fff'//值得颜色
                                     }
                                 }
                             }
                         },
                         data: this.list.xData
                     },
                 ]
            };


            this.statistics.chart = EChart.init(this.$refs.statistics)
            this.statistics.chart.setOption(this.statistics.option)
        },
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
.testEcharts{
    border-right:0;
    border-left: 0;
    width:50%;
    height:400px;
    /* background-color: red; */
}
</style>
