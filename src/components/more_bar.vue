<template>
  <div class="hello">
    <div class="testEcharts" ref="statistics"></div>
  </div>
</template>

<script>
  import EChart from 'echarts'

  export default {
    props: {
      list: {
        type: Object,
        default: () => {
          return {}
        }
      }
    },
    data() {
      return {
        statistics: {
          option: {},
          chart: {},
          element: {},
        },
      }
    },
    mounted() {
      this.initData();
      window.onresize = () => {
        this.statistics.chart.resize();
      }
    },
    destory() {
      window.onresize = null;
    },
    methods: {
      initData() {
        let vue = this;
        var colorList = [
          '#ff7f50', '#87cefa', '#da70d6', '#32cd32', '#6495ed',
          '#ff69b4', '#ba55d3', '#cd5c5c', '#ffa500', '#40e0d0'
        ];
        this.statistics.option = {
          // title: {
          //      text: '2010-2013年中国城镇居民家庭人均消费构成（元）',
          // },
          tooltip: {
            trigger: 'axis',
            // backgroundColor: 'rgba(255,255,255,0.7)',
            axisPointer: {
              type: 'shadow'
            },
            textStyle: {
              color: 'rgba(255,255,255,0.7)'
            }
            // formatter: function(params) {
            //   console.log(params,'params')
            //     var color = colorList[params[0].dataIndex];
            //     var res = '<div style="color:' + color + '">';
            //     res += '<strong>' + params[0].name + '个</strong>'
            //     for (var i = 0, l = params.length; i < l; i++) {
            //         res += '<br/>' + params[i].seriesName + ' : ' + params[i].value
            //     }
            //     res += '</div>';
            //     return res;
            // }
          },
          legend: {
            align: 'right',
            right: '10%',
            textStyle: {
              color: 'rgba(255,255,255,0.7)'
            },
            data: ['高风险', '中风险', '低风险']
          },
          // toolbox: {
          //     show: true,
          //     orient: 'vertical',
          //     y: 'center',
          //     feature: {
          //         mark: {show: true},
          //         dataView: {show: true, readOnly: false},
          //         restore: {show: true},
          //         saveAsImage: {show: true}
          //     }
          // },
          calculable: true,
          grid: {
            // y: 30,
            // y2: 30,
            // x2: 10
            top: '20%',
            left: '15%',
            bottom: '15%',
            right: '8%'
          },
          xAxis: [
            {
              type: 'category',
              // data: vue.list.name,
              data: ['教育行业', '医疗行业', '古建行业'],
              name: '(个)',
              nameLocation: 'start',
              nameTextStyle: {
                color: 'rgba(255,255,255,0.7)',
                padding: [0, 5, 0, 0]
              },
              axisLabel: {
                color: 'rgba(255,255,255,0.7)'
              }
            }
          ],
          yAxis: [
            {
              type: 'value',
              zlevel: 0,
              axisLabel: {
                color: 'rgba(255,255,255,0.7)'
              },
              splitLine: {
                show:false,
                lineStyle: {
                  color: 'rgba(28, 47, 91, 0.7)'
                }
              },
              // splitArea: {
              //   show: true,
              //   areaStyle: {
              //     color: ['rgba(18, 34, 59, 0.7)', 'rgba(18, 34, 59, 0.1)']
              //   }
              // }
            }
          ],
          series: [
            {
              name: '高风险',
              type: 'bar',
              zlevel: 1,
              barWidth: 10,
              itemStyle: {
                normal: {
                  color: new EChart.graphic.LinearGradient(1, 1, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                    offset: 0,
                    color: 'rgba(244,69,81,0.1)'
                  }, {
                    offset: 0.6,
                    color: 'rgba(244,69,81,0.5)'
                  }, {
                    offset: 1,
                    color: 'rgba(244,69,81,1)'
                  }])
                },
                opacity: 0.5
              },
              // data: vue.list.high
              data: [4804.7,1444.3,1332.1]
            },
            {
              name: '中风险',
              type: 'bar',
              zlevel: 1,
              barWidth: 10,
              itemStyle: {
                normal: {
                  color: new EChart.graphic.LinearGradient(1, 1, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                    offset: 0,
                    color: 'rgba(242,169,2,0.1)'
                  }, {
                    offset: 0.6,
                    color: 'rgba(242,169,2,0.5)'
                  }, {
                    offset: 1,
                    color: 'rgba(242,169,2,1)'
                  }])
                },
                opacity: 0.5
              },
              // itemStyle: itemStyle,
              // data: vue.list.center
              data: [5506.3,1674.7,1405]
            },
            {
              name: '低风险',
              type: 'bar',
              zlevel: 1,
              barWidth: 10,
              itemStyle: {
                normal: {
                  color: new EChart.graphic.LinearGradient(1, 1, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                    offset: 0,
                    color: 'rgba(19,221,191,0.1)'
                  }, {
                    offset: 0.6,
                    color: 'rgba(19,221,191,0.5)'
                  }, {
                    offset: 1,
                    color: 'rgba(19,221,191,1)'
                  }])
                },
                opacity: 0.5
              },
              // itemStyle: itemStyle,
              // data: vue.list.low
              data: [6040.9,1823.4,1484.3]
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
    height: 200px;
    /* background-color: red; */
  }
</style>
