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
            var i=0;
            var colors=['#3f5fe9','#3fd2bf','#dc1f65','#fd9924', "#35B9BC","#E7536B"];
            this.statistics.option = {
              tooltip: {
                  // trigger: 'item',
                  // formatter: "{a} <br/>{b}: {c} ({d}%)",
                  // show:true,
                  trigger: 'item',
                  formatter: "{b} : {d}% <br/> {c}"
              },

              // color:[
              //   "rgba(128, 128, 128, 0.5)",
              //   "#F28051",
              //   "#A682E6",
              //   "#329AE6",
              //   "#35B9BC",
              //   "#E7536B",
              //   "#59F8CB",
              //   "#2C9FFF",
              //   "#97F7EC",
              //   "#417AFE",
              //   "#2DDAF8",
              //   " #0CE0F2",
              //   "#C780ED",
              //   " #FF3469",
              //   "#FF4242",
              //   "#FA94B2",
              //   "#FFC835",
              //   "#FFDC7A"
              // ],
              legend: {
                orient: "vertical",
                show: true,
                right: 0,
                top: 20,
                // bottom: 10,
                textStyle: {
                  width: 50,
                  color:'#fff',  //字体颜色
                },
                  // data:this.list.legend_data
                  // ['住宅','人员密集场所','交通工具','垃圾及废弃物','农副业场所','物资仓储场所','其他']
                  data: [
                    {
                      name: '住宅',
                      // 强制设置图形为圆。
                      icon: 'image://../../static/logo.png',
                      // icon: 'image://data:image/gif;base64,R0lGODlhEAAQAMQAAORHHOVSKudfOulrSOp3WOyDZu6QdvCchPGolfO0o/XBs/fNwfjZ0frl3/zy7////wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACH5BAkAABAALAAAAAAQABAAAAVVICSOZGlCQAosJ6mu7fiyZeKqNKToQGDsM8hBADgUXoGAiqhSvp5QAnQKGIgUhwFUYLCVDFCrKUE1lBavAViFIDlTImbKC5Gm2hB0SlBCBMQiB0UjIQA7',
                      // 设置文本为红色
                      // textStyle: {
                      //     color: 'red'
                      // }
                    },{
                        name: '人员密集场所',
                        // 强制设置图形为圆。
                        // icon: 'arrow',
                        // 设置文本为红色
                        // textStyle: {
                        //     color: 'red'
                        // }
                      },{
                        name: '交通工具',
                        // 强制设置图形为圆。
                        // icon: 'circle',
                        // 设置文本为红色
                        // textStyle: {
                        //     color: 'red'
                        // }
                      },{
                        name: '垃圾及废弃物',
                        // 强制设置图形为圆。
                        // icon: 'circle',
                        // 设置文本为红色
                        // textStyle: {
                        //     color: 'red'
                        // }
                      },{
                        name: '农副业场所',
                        // 强制设置图形为圆。
                        // icon: 'circle',
                        // 设置文本为红色
                        // textStyle: {
                        //     color: 'red'
                        // }
                      },{
                        name: '物资仓储场所',
                        // 强制设置图形为圆。
                        // icon: 'circle',
                        // 设置文本为红色
                        // textStyle: {
                        //     color: 'red'
                        // }
                      },
                      {
                        name: '其他',
                        // 强制设置图形为圆。
                        // icon: 'circle',
                        // 设置文本为红色
                        // textStyle: {
                        //     color: 'red'
                        // }
                      }
                    ]
              },
              series: [
                  {
                      type:'pie',
                      radius: ['50%', '70%'],
                      avoidLabelOverlap: true,
                      itemStyle : {
                          normal : {
                              color:function(){
                                  return colors[i++];
                                  },
                              label : {
                                  show : false
                              },
                              labelLine : {
                                  show : false
                              }
                          },
                          emphasis : {
                              label : {
                                  show : true,
                                  position : 'center',
                                  textStyle : {
                                      fontSize : '30',
                                      fontWeight : 'bold'
                                  }
                              }
                          }
                      },

                      label: {
                            normal: {
                              show: true,
                              // formatter: '{b} : {c} \n ({d}%)',  //带有显示数量
                              // formatter: '{b}\n\n {d}%',
                              formatter: function(params){
                                console.log(params)
                                let seriesName = params.name;
                                let percent = params.percent;
                                let result = `{a|${seriesName}\n${percent}%}`;
                                return result;
                                  // return `${seriesName}\n${percent}`
                              },


                              /*demo*/
                              // formatter: '{c|{c}}\n{hr|}\n{d|{d}%}',
                              // rich: {
                              //     b: {
                              //         fontSize: 16,
                              //         color: '#12EABE',
                              //         align: 'left',
                              //         padding: 4
                              //     },
                              //     hr: {
                              //         borderColor: '#12EABE',
                              //         width: '100%',
                              //         borderWidth: 1,
                              //         height: 0
                              //     },
                              //     d: {
                              //         fontSize: 16,
                              //         color: '#fff',
                              //         align: 'left',
                              //         padding: 4
                              //     },
                              //     c: {
                              //         fontSize: 16,
                              //         color: '#fff',
                              //         align: 'left',
                              //         padding: 4
                              //     }
                              // }

                              color:'white',
                              rich: {
                                  a: {
                                      color: '#fff',
                                      fontSize: 11,
                                      lineHeight: 20,
                                      align: 'left',
                                  },
                                  hr: {
                                      width: '100%',
                                      height: 0,
                                      alien:'left'
                                  },
                              }
                          }
                      },
                      labelLine: {

                          normal: {
                              show: true,
                              length:10,
                              length2:40,
                              lineStyle :{
                                type:'solid',
                              }
                          },
                      },
                      data:[
                          {
                            value:600,
                            name:'住宅',
                            icon:'../../static/logo.png',
                            itemStyle:{
                                normal:{
                                    color: new EChart.graphic.LinearGradient(1, 1,0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                        offset: 1,
                                        color: '#2a99fa'
                                    }, {
                                        offset: 0.6,
                                        color: '#1c65a4'
                                    },{
                                        offset: 0,
                                        color: 'black'
                                    }])
                                }
                            },
                            labelLine: {
                                normal: {
                                    lineStyle :{
                                      color: '#2a99fa'
                                    }
                                },
                            },
                           },
                          {
                            value:900,
                            name:'人员密集场所',
                            itemStyle:{
                                normal:{
                                    color: new EChart.graphic.LinearGradient(1, 0,0, 1, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                        offset: 0.2,
                                        color: '#0197a3'
                                    }, {
                                        offset: 0.5,
                                        color: '#026c77'
                                    },{
                                        offset: 0.85,
                                        color: 'rgba(0,0,0,0.9)'
                                    },{
                                        offset: 1,
                                        color: 'black'
                                    }])
                                }
                            },
                            labelLine: {
                                normal: {
                                    lineStyle :{
                                      type:'solid',
                                      color: '#0197a3'
                                    }
                                },
                            },
                          },
                          {
                            value:1000,
                            name:'交通工具',
                            itemStyle:{
                                normal:{
                                    color: new EChart.graphic.LinearGradient(1, 1, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                        offset: 0.2,
                                        color: '#42b64b'
                                    }, {
                                        offset: 0.5,
                                        color: '#2b7737'
                                    },{
                                        offset: 0.85,
                                        color: 'rgba(0,0,0,0.9)'
                                    }, {
                                        offset: 1,
                                        color: 'black'
                                    }])
                                }
                            },
                            labelLine: {
                                normal: {
                                    lineStyle :{
                                      color: '#42b64b'
                                    }
                                },
                            },
                        },
                          {
                            value:320,
                            name:'垃圾及废弃物',
                            itemStyle:{
                                normal:{
                                    color: new EChart.graphic.LinearGradient(1, 1, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                        offset: 0.2,
                                        color: '#dfb040'
                                    }, {
                                        offset: 0.5,
                                        color: '#6a5a2a'
                                    },{
                                        offset: 0.85,
                                        color: 'rgba(0,0,0,0.9)'
                                    }, {
                                        offset: 1,
                                        color: 'black'
                                    }])
                                }
                            },
                            labelLine: {
                                normal: {
                                    lineStyle :{
                                      color: '#dfb040'
                                    }
                                },
                            },
                        },
                          {
                            value:150,
                            name:'农副业场所',
                            itemStyle:{
                                normal:{
                                    color: new EChart.graphic.LinearGradient(1, 1, 1, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                        offset: 0.2,
                                        color: '#bd433e'
                                    }, {
                                        offset: 0.5,
                                        color: '#702e2e'
                                    },{
                                        offset: 0.85,
                                        color: 'rgba(0,0,0,0.9)'
                                    }, {
                                        offset: 1,
                                        color: 'black'
                                    }])
                                }
                            },
                            labelLine: {
                                normal: {
                                    lineStyle :{
                                      color: '#bd433e'
                                    }
                                },
                            },
                        },
                          {
                            value:400,
                            name:'物资仓储场所',
                            itemStyle:{
                                normal:{
                                    color: new EChart.graphic.LinearGradient(0, 1, 1, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                        offset: 0.2,
                                        color: '#892ee4'
                                    }, {
                                        offset: 0.5,
                                        color: '#381c68'
                                    },{
                                        offset: 0.85,
                                        color: 'rgba(0,0,0,0.9)'
                                    }, {
                                        offset: 1,
                                        color: 'black'
                                    }])
                                }
                            },
                            labelLine: {
                                normal: {
                                    lineStyle :{
                                      color: '#892ee4'
                                    }
                                },
                            },
                        },
                          {
                            value:0,
                            name:'其他',
                            itemStyle:{
                                normal:{
                                    color: new EChart.graphic.LinearGradient(0, 1, 1, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                        offset: 0.2,
                                        color: '#7e6570'
                                    }, {
                                        offset: 0.5,
                                        color: '#433b45'
                                    },{
                                        offset: 0.85,
                                        color: 'rgba(0,0,0,0.9)'
                                    }, {
                                        offset: 1,
                                        color: 'black'
                                    }])
                                }
                            },
                            labelLine: {
                                normal: {
                                    lineStyle :{
                                      color: '#7e6570'
                                    }
                                },
                            },
                        }
                      ]
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
