<template>
  <div class="hello">
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
            var colors=['#3f5fe9','#3fd2bf','#dc1f65','#fd9924'];
            this.statistics.option = {
              // tooltip: {
              //     trigger: 'item',
              //     formatter: "{b} : {d}% <br/> {c}"
              // },
              graphic: {
                  elements: [{
                      type: 'image',
                      style: {
                          image: '../../static/logo.png',
                          width: 70,
                          height: 70
                      },
                      left: 'center',
                      top: 'center'
                  }]
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
                  // color:'#fff',  //字体颜色
                },
                  data:['高风险','中风险','低风险']
                  // data:[
                  //   {
                  //     name:'高风险',
                  //     icon: 'image://../../static/logo.png',
                  //   }
                  // ]
              },
              series: [
                  {
                      type:'pie',
                      radius: ['50%', '70%'],
                      // center: ['50%', '50%'],
                      // avoidLabelOverlap: true,
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
                      data:[
                            {
                              value:400,
                              name:'高风险',
                              itemStyle:{
                                  normal:{
                                      color: new EChart.graphic.LinearGradient(1, 1, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                          offset: 1,
                                          color: '#892ee4'
                                      }, {
                                          offset: 0.6,
                                          color: '#381c68'
                                      } ,{
                                          offset: 0,
                                          color: 'black'
                                      }])
                                  }
                              },
                          },
                          {
                            value:150,
                            name:'中风险',
                            itemStyle:{
                                normal:{
                                    color: new EChart.graphic.LinearGradient(1, 1, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

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
                        },
                        {
                          value:320,
                          name:'低风险',
                          itemStyle:{
                              normal:{
                                  color: new EChart.graphic.LinearGradient(1, 1, 1, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                      offset: 0.2,
                                      color: '#dfb040'
                                  }, {
                                      offset: 0.5,
                                      color: '#6a5a2a'
                                  },{
                                      offset: 0.95,
                                      color: 'rgba(0,0,0,1)'
                                  }, {
                                      offset: 1,
                                      color: 'black'
                                  }])
                              }
                          },
                      },

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
