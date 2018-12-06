<template>
  <div class="hello">
    <div class="testEcharts" ref="statistics"></div>
  </div>
</template>

<script>
  import EChart from 'echarts'

  export default {
    props: ["XData", "YData"],
    data() {
      return {
        statistics: {
          option: {},
          chart: {},
          element: {},
        }
      }
    },
    mounted() {
      this.$nextTick(() => {
        this.initData();
      })
      window.onresize = () => {
        this.statistics.chart.resize();
      }
    },
    destory() {
      window.onresize = null;
    },
    methods: {
      initData() {
        var data = [{
                        "name": "11-12",
                        "value": 80
                    }, {
                        "name": "11-13",
                        "value": 87
                    }, {
                        "name": "11-14",
                        "value": 71
                    }, {
                        "name": "11-15",
                        "value": 80
                    }, {
                        "name": "11-16",
                        "value": 66
                    }, {
                        "name": "11-17",
                        "value": 80
                    }, {
                        "name": "11-18",
                        "value": 80
                    }];
                    var xData = [],
                        yData = [];
                    var min = 0;
                    data.map(function(a, b) {
                        xData.push(a.name);
                        if (a.value === 0) {
                            yData.push(a.value + min);
                        } else {
                            yData.push(a.value);
                        }
                    });
                    let max = Math.max.apply(null, yData)+10;

        this.statistics.option = {
          // backgroundColor:"#111c4e",
          color: ['#3398DB'],
          tooltip: {
              trigger: 'axis',
              axisPointer: {
                  type: 'line',
                  lineStyle: {
                      opacity: 0
                  }
              },
              formatter: function(prams) {
                  if (prams[0].data === min) {
                      return "报警数：0"
                  } else {
                      return "报警数：" + prams[0].data
                  }
              }
          },
          legend: {
              data: ['报警数', '背景'],
              show: false
          },
          grid: {
              left: '0%',
              right: '0%',
              bottom: '5%',
              top: '7%',
              height: '85%',
              containLabel: true,
              z: 22
          },
          xAxis: [{
              type: 'category',
              gridIndex: 0,
              data: xData,
              boundaryGap: true,
              // 是否显示坐标刻度
              axisTick: {
                  show:false
              },
              axisLine: {
                   lineStyle: {
                       color: '#0d5672'
                   }
               },
              splitLine: {
                  // interval:1,
                  show: true,
                  lineStyle:{
                       color:'#071f2a',
                       width: 1,
                      type: 'solid'
                  }
              },
              axisLabel: {
                   show: true,
                   color:'#979797',
                   fontSize:12
              }
          }],
          yAxis: [
              {
                  type: 'value',
                  name:'（起）',
                  gridIndex: 0,
                  nameLocation: 'start',
                  nameTextStyle: {
                    color: '#979797',
                    fontSize: 14,
                    padding: [-21, 60, 0, 0]
                    // padding: [0,0,30,0]
                  },
                  splitLine: {
                      show: false
                  },
                  // 是否显示坐标刻度
                  axisTick: {
                      show: true
                  },
                  axisLine: {
                    lineStyle: {
                        color: '#979797'
                    }
                  },
                  min: min,
                  // max: max,
                  axisLabel: {
                      color: '#979797',
                      fontSize:14,
                      formatter: '{value}'
                  }
              },
              {
                  type: 'value',
                  gridIndex: 0,
                  min: min,
                  max: max,
                  // splitNumber: 12,
                  splitLine: {
                      // interval:1,
                      show: true,
                      lineStyle:{
                           color:'#071f2a',
                           width: 1,
                          type: 'solid'
                      }
                  },
                  axisLine: {
                      show: true,
                      lineStyle: {
                          color: '#071f2a'
                      }

                  },
                  axisTick: {
                      show: false
                  },
                  axisLabel: {
                      show: false
                  },
                  // splitArea: {
                  //     show: true,
                  //     areaStyle: {
                  //         color: ['rgba(250,250,250,0.0)', 'rgba(250,250,250,0.05)']
                  //     }
                  // }
              }
          ],
          series: [
            {
                name: '背景',
                type: 'bar',
                barWidth: '45%',
                xAxisIndex: 0,
                yAxisIndex: 1,
                barGap: '-83%',
                data: [max, max, max, max, max, max, max],
                itemStyle: {
                  normal: {
                    color: 'rgba(28, 48, 91, 0.5)',
                    borderColor:'rgba(28, 47, 91, 0.7)',
                    borderWidth:1
                  }
                },
                zlevel: 9
            },
            {
                  name: '报警数',
                  type: 'bar',
                  barWidth: '20',
                  xAxisIndex: 0,
                  yAxisIndex: 0,
                  itemStyle: {
                      normal: {
                          color: new EChart.graphic.LinearGradient(
                              0, 0, 0, 1, [{
                                      offset: 0,
                                      color: '#01a49f'
                                  },
                                  {
                                      offset: 0.5,
                                      color: '#066e74'
                                  },
                                  {
                                      offset: 1,
                                      color: '#0b3142'
                                  }
                              ]
                          )
                      }
                  },
                  data: yData,
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
  .testEcharts {
    border-right: 0;
    border-left: 0;
    width: 524px;
    height: 220px;
    /* background-color: red; */
  }
</style>
