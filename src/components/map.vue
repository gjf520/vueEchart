<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <h2>Ecosystem</h2> -->
    <!-- <div class="testEcharts" ref="statistics"></div> -->
    <div id="map-wrap" style="height: 500px;">
		<!-- 这里以后是地图 -->
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
            this.echarts.registerMap('china', this.chinaJson);
            this.statistics.option = {

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
    width:50%;
    height:300px;
    /* background-color: red; */
}
</style>
