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
            align: 'left',
            right: '10%',
            textStyle: {
              color: 'rgba(255,255,255,0.7)'
            },
            data: ['水压', '风压', '防火门','离位']
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
              data: ['mon', 'tue', 'wed','thu','fri','sat','sun'],
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
              name: '水压',
              type: 'bar',
              zlevel: 1,
              // barWidth: 10,
              itemStyle: {
                normal: {
                  color: 'blue'
                },
                opacity: 0.5
              },
              // data: vue.list.high
              data: [7,6,8,6,2,4,6]
            },
            {
              name:  '风压',
              type: 'bar',
              zlevel: 1,
              // barWidth: 10,
              itemStyle: {
                normal: {
                  color: 'green'
                },
                opacity: 0.5
              },
              // itemStyle: itemStyle,
              // data: vue.list.center
              data: [7,4,8,7,1,4,6]
            },
            {
              name: '防火门',
              type: 'bar',
              zlevel: 1,
              // barWidth: 10,
              itemStyle: {
                normal: {
                  color: 'red'
                },
                opacity: 0.5
              },
              // itemStyle: itemStyle,
              // data: vue.list.low
              data: [7,6,2,6,5,4,6]
            },{
              name: '离位',
              type: 'bar',
              zlevel: 1,
              // barWidth: 10,
              itemStyle: {
                normal: {
                  color: 'skyblue'
                },
                opacity: 0.5
              },
              // itemStyle: itemStyle,
              // data: vue.list.low
              data: [3,6,2,6,2,7,6]
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
