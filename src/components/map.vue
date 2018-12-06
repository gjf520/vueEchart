<template>
  <div class="amap-page-container">
      <el-amap vid="amapDemo" :zoom="zoom" :center="center" class="amap-demo" :plugin="plugin">
        <el-amap-info-window  :position="mywindow.position" :content="mywindow.content" :visible="mywindow.visible" :events="mywindow.events"></el-amap-info-window>
        <el-amap-marker :position="marker.position" :label='label' :events="marker.events" :visible="marker.visible" :draggable="marker.draggable"></el-amap-marker>
        <el-amap-circle :center="circle.center" :radius="circle.radius" :fillOpacity="circle.fillOpacity" :events="circle.events" :strokeColor="circle.strokeColor" :strokeStyle="circle.strokeStyle" :fillColor="circle.fillColor"></el-amap-circle>

      </el-amap>
  </div>
</template>

<script>
import EChart from 'echarts'

export default {
  data () {
    return {
      zoom: 15,
      center: [121.5273285, 31.21515044],
      // label:{
      // content:'钦汇园',
      //   offset:[10,12]
      // },
      address: '',
         events: {
           click(e) {
             let { lng, lat } = e.lnglat;
             self.lng = lng;
             self.lat = lat;

             // 这里通过高德 SDK 完成。
             var geocoder = new AMap.Geocoder({
               radius: 1000,
               extensions: "all"
             });
             geocoder.getAddress([lng ,lat], function(status, result) {
               if (status === 'complete' && result.info === 'OK') {
                 if (result && result.regeocode) {
                   self.address = result.regeocode.formattedAddress;
                   self.$nextTick();
                 }
               }
             });
           }
         },
         lng: 0,
         lat: 0,

      circle: {
        clickable: true,
        center: [121.5273285, 31.21515044],
        radius: 200,
        fillOpacity: 0.3,
        strokeStyle: 'dashed',
        fillColor: '#FFFF00',
        strokeColor: '#00BFFF'
      },
      marker: {
        position: [121.5273285, 31.21515044],
        events: {
          click: () => {
            if (this.mywindow.visible === true) {
              this.mywindow.visible = false
            } else {
              this.mywindow.visible = true
            }
          },
          dragend: (e) => {
            this.markers[0].position = [e.lnglat.lng, e.lnglat.lat]
          }
        },
        visible: true,
        draggable: false
      },
      mywindow: {
        position: [121.5273285, 31.21515044],
        content: '葛建芳葛建芳葛建芳葛建芳葛建芳葛建芳',
        visible: true,
        events: {
          close () {
            // this.mywindow.visible = false
          }
        }
      },
      plugin: {
        pName: 'Scale',
        events: {
          init (instance) {
            console.log(instance)
          }
        }
      }
    }
  }
}
</script>
<style scoped>
.amap-page-container {
    height: 500px;
  }
</style>
