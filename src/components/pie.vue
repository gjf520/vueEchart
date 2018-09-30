<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <h2>Ecosystem</h2> -->
    <div class="pieEcharts" ref="statistics"></div>
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
              tooltip: {
                  trigger: 'item',
                  // formatter: "{a} <br/>{b}: {c} ({d}%)"
              },
              color:[
                "#F28051",
                "#A682E6",
                "#329AE6",
                "#35B9BC",
                "#E7536B",
                "#59F8CB",
                "#2C9FFF",
                "#97F7EC",
                "#417AFE",
                "#2DDAF8",
                " #0CE0F2",
                "#C780ED",
                " #FF3469",
                "#FF4242",
                "#FA94B2",
                "#FFC835",
                "#FFDC7A"
              ],
              legend: {
                orient: "vertical",
                show: true,
                right: 0,
                top: 20,
                // bottom: 10,
                textStyle: {
                  width: 50,
                  color:'#fff',
                },
                  data:this.list.legend_data
              },
              series: [
                  {
                      type:'pie',
                      radius: ['50%', '70%'],
                      avoidLabelOverlap: true,
                      label: {
                        normal: {
                            // formatter: '{a|{a}}{abg|}\n{hr|}\n  {b|{b}：}{c}  {per|{d}%}  ',
                            formatter: '{a|{b}}\n{hr|}\n{per|{d}%}',
                            // formatter: '{b} : {c} \n ({d}%)',  //带有显示数量
                            // formatter: '{b}\n ({d}%)',
                            rich: {
                                a: {
                                    color: '#fff',
                                    fontSize: 11,
                                    lineHeight: 20,
                                    align: 'center'
                                },
                                hr: {
                                    width: '100%',
                                    height: 0,
                                    alien:'center'
                                },
                                per: {
                                    color: '#fff',
                                    align: 'center',
                                    fontSize: 15,
                                }
                            }
                        },           
                    },

//                       label: {
//                             normal: {
//                               show: true,
//                               // formatter: '{b} : {c} \n ({d}%)',  //带有显示数量
//                               formatter: '{b}\n ({d}%)',
//                               rich: {
//                         a: {
//                             color: '#fff',
//                             fontSize: 11,
//                             lineHeight: 20,
//                             align: 'center'
//                         },
// //                         hr: {
// //                             width: '100%',
// //                             height: 0,
// //                             alien:'center'
// //                         },
// //                         per: {
// //                             color: '#000000',
// //                             align: 'center',
// //                             fontSize: 15,
// //                         }
//                       }
//
//                           }
//                         },
                      labelLine: {
                          normal: {
                              show: true,
                              lineStyle :{
                                color:'#fff'
                              }
                          },
                      },
                      data:this.list.series_data
                  }
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
.pieEcharts{
    border-right:0;
    border-left: 0;
    width:50%;
    height:300px;
    /* background-color: red; */
}
</style>
