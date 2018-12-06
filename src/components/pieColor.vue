<!--
    by: wlwang  2018/10/26
    name: 饼图组件
    notes:
-->
<template>
    <div class="pieChartBox">
        <div class="pieChartCon" ref="pieChartCon"></div>
    </div>
</template>

<script>
import EChart from 'echarts';
export default {
    data () {
        return {
            pieChartCon:{
                option: {},
                chart: {},
                element: {}
            },
            chartArray: ['pieChartCon'],//需要销毁的echarts图标
        }
    },
    mounted() {
        this.drawAllChart(); //初始化echarts实例
        let that = this
        window.onresize = function () {
            that.disposeAllChart();// 销毁echarts实例对象 重新加载
        }
    },
    destory(){
        window.onresize = null
    },
    methods: {
        drawAllChart(){
            var i=0;
            var colors=['#3f5fe9','#3fd2bf','#dc1f65','#fd9924'];
            this.pieChartCon.option = {
                tooltip: {
                    trigger: 'item',
                    formatter: "{a} <br/>{b}: {c} ({d}%)"
                },
                legend: {
                    orient: 'vertical',
                    x: 'left',
                    data:['直接访问','邮件营销','联盟广告','视频广告']
                },
                calculable : true,
                series: [
                    {
                        name:'访问来源',
                        type:'pie',
                        radius: ['50%', '70%'],
                        avoidLabelOverlap: false,
                        // startAngle:-135,
                        // endAngle: 135,
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
                                show: false,
                                position: 'center'
                            },
                            emphasis: {
                                show: true,
                                textStyle: {
                                    fontSize: '30',
                                    fontWeight: 'bold'
                                }
                            }
                        },
                        labelLine: {
                            normal: {
                                show: false
                            }
                        },
                        data:[
                            {value:335, name:'直接访问111',
                                itemStyle:{
                                    normal:{
                                        color: new EChart.graphic.LinearGradient(1, 0, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                            offset: 0,
                                            color: '#3f5fe9'
                                        }, {
                                            offset: 1,
                                            color: '#66ccff'
                                        }])
                                    }
                                }
                            },
                            {value:310, name:'邮件营销',itemStyle:{
                            normal:{
                                color: new EChart.graphic.LinearGradient(1, 0, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                    offset: 0,
                                    color: '#99ffcc'
                                }, {
                                    offset: 1,
                                    color: '#3fd2bf'
                                }])
                            }
                        }},
                            {value:234, name:'联盟广告',
                                itemStyle:{
                                    normal:{
                                        color: new EChart.graphic.LinearGradient(1, 0, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                            offset: 0,
                                            color: '#ff6633'
                                        }, {
                                            offset: 1,
                                            color: '#dc1f65'
                                        }])
                                    }
                                }
                            },
                            {value:135, name:'视频广告',
                                itemStyle:{
                                    normal:{
                                        color: new EChart.graphic.LinearGradient(1, 0, 0, 0, [{ //颜色渐变函数 前四个参数分别表示四个位置依次为左、下、右、上

                                            offset: 0,
                                            color: '#ffcc33'
                                        }, {
                                            offset: 1,
                                            color: '#fd9924'
                                        }])
                                    }
                                }
                            }
                        ]
                    }
                ]
            };
            this.pieChartCon.chart = EChart.init(this.$refs.pieChartCon)
            this.pieChartCon.chart.setOption(this.pieChartCon.option)
        },
        //释放图表，销毁对象
        disposeAllChart(){
            let i = 0 , len = this.chartArray.length
            for (;i < len; i++){
                let a = this.chartArray[i]
                if(this[a].chart){
                    this[a].chart.dispose()
                }
            }
            this.drawAllChart()
        }
    }
}
</script>
<style lang="less" scoped>
@import "~@/libs/css/theme/theme.less";
.pieChartCon{
    width:100%;
    min-height:300px;
    overflow-y: auto;
    text-align: center;
}
</style>
