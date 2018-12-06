<template>
  <div class="hello">
    <div class="testEcharts" ref="statistics">

    </div>
    <div class='precent' >
      <p  class='item' v-for='(item,index) in percent' :key='index'>
        {{(item * 100).toFixed(1) }}%
      </p>
    </div>
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
          percent:[0.50, 0.34, 0.67, 0.666, 0.888],
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
          var baifenbi = [0.50, 0.34, 0.67, 0.666, 0.888];
          var grayBar = [1, 1, 1, 1, 1];
          var zongjine = [1, 1, 1, 1,1];
          var xingm = ['召陵人民医院', '召陵人民医院', '新城区人民医院', '新城区中医院', '民政康复医院'];
            this.statistics.option = {
                  // backgroundColor: '#061A42',
                  color: ['#61A8FF'], //进度条颜色
                  /* grid: {
                       left: '-10%',  //如果离左边太远就用这个......
                       //right: '14%',
                       bottom: '5%',
                       top: '5%',
                       containLabel: true
                   },*/
                  xAxis: [
                      {
                          show: false,
                      },
                      //由于下边X轴已经是百分比刻度了,所以需要在顶部加一个X轴,刻度是金额,也隐藏掉
                      {
                          show: false,
                      },

                  ],
                  yAxis: {
                      type: 'category',
                      axisLabel: {
                          show: false, //让Y轴数据不显示
                      },
                      itemStyle: {

                      },
                      axisTick: {
                          show: false, //隐藏Y轴刻度
                      },
                      axisLine: {
                          show: false, //隐藏Y轴线段
                      },
                      data: xingm,
                  },
                  series: [
                      //背景色--------------------我是分割线君------------------------------//
                      {
                          show: true,
                          type: 'bar',
                          barGap: '-100%',
                          barWidth: '35%', //统计条宽度
                          itemStyle: {
                              normal: {
                                barBorderRadius: false,
                                color: 'rgba(102, 102, 102,0.5)'
                              },
                          },
                          z: 1,
                          data: grayBar,
                      },
                      //蓝条--------------------我是分割线君------------------------------//
                      {
                          show: true,
                          type: 'bar',
                          barGap: '-100%',
                          barWidth: '35%', //统计条宽度
                          itemStyle: {
                              normal: {
                                  color: {
                                      type: 'bar',
                                      colorStops: [{
                                          offset: 0,
                                          color: '#122a40' // 0% 处的颜色
                                      }, {
                                          offset: 1,
                                          color: '#0292f4' // 100% 处的颜色
                                      }],
                                      globalCoord: false, // 缺省为 false

                                  }
                              },
                          },
                          max: 1,
                          // label: {
                          //     normal: {
                          //         show: true,
                          //         textStyle: {
                          //             color: '#fff', //百分比颜色
                          //         },
                          //         position: 'inside',
                          //         //百分比格式
                          //         formatter: function(data) {
                          //             return (baifenbi[data.dataIndex] * 100).toFixed(1) + '%';
                          //         },
                          //     }
                          // },
                          labelLine: {
                              show: true,
                          },
                          z: 2,
                          data: baifenbi,
                      },
                      //数据条--------------------我是分割线君------------------------------//
                      {
                          show: true,
                          type: 'bar',
                          xAxisIndex: 1, //代表使用第二个X轴刻度!!!!!!!!!!!!!!!!!!!!!!!!
                          barGap: '-100%',
                          barWidth: '40%', //统计条宽度
                          itemStyle: {
                              normal: {
                                  barBorderRadius: false,
                                  color: 'rgba(22,203,115,0.05)'
                              },
                          },
                          label: {
                              normal: {
                                  show: true,
                                  //label 的position位置可以是top bottom left,right,也可以是固定值
                                  //在这里需要上下统一对齐,所以用固定值
                                  position: [-1, '-120%'],
                                  width:80,
                                  padding:[1,10,0,1],
                                  rich: { //富文本
                                      a: {
                                         align:'left',
                                      },
                                      white: { //自定义颜色
                                          color: '#ffffff',
                                      },
                                      green: {
                                          color: '#70DDA7',
                                      },
                                      yellow: {
                                          color: '#CCB877',
                                      },
                                      red: {
                                          color: '#BC3C47',
                                      },
                                      gray: {
                                          color: '#727CBA'
                                      },
                                      blue:{
                                        color:'#12629b'
                                      },
                                      start2: {
                                        	width:80,
                                					align:'center',
                                          backgroundColor: { //这里可以添加你想自定义的图片
                                              // image: backgroundImage1,
                                          },
                                        },
                                      start1: {
                                      	width:350,
                              					align:'center',
                                        backgroundColor: {
                                            // image: backgroundImage2,
                                        }
                                      }
                                  },
                                  formatter: function(data) {
                                      //富文本固定格式{colorName|这里填你想要写的内容}
                                          // return '{white|' +'  ' + xingm[data.dataIndex] + '}'+''+'{start1|}{blue|'+'  '+ (baifenbi[data.dataIndex] * 100).toFixed(1) + '%' + '}';
                                          return '{white|' +'  ' + xingm[data.dataIndex] + '}'
                                  },
                              }
                          },
                          data: zongjine
                      }

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
    width:350px;
    height:300px;
    /* background-color: red; */
}
.hello{
  position: relative;
}
.precent{
  font-size: 12px;
  color: #12629b;
  position: absolute;
  top: 44px;
  left: 263px;
  width: 70px;

  }
  .item{
    margin-bottom: 22px;
}
</style>
