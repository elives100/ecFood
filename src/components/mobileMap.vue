<template>
  <div>
    <l-map class="test" @click="closePanel()" :options="{scrollWheelZoom:false}"  style="height: 100vh" :zoom="zoom" :center="center">
      <l-tile-layer :url="url"></l-tile-layer>
      <div v-for="(marker, index) in markerLatLng" :key="index">
        <l-marker v-model="check" @click="markerClick(marker)" :lat-lng="marker.coord"></l-marker>
      </div>
    </l-map>
  </div>
</template>

<script>
import { bus } from "../main.js";

export default {
  data() {
    return {
      check: "",
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      zoom: 7,
      center: [39.988757,-75.847020],
      markerLatLng: [
        {coord: [40.5187,-78.3947]},
        {coord: [40.6884, -75.2207]},
        {coord: [40.630891,-73.963590]},
        {coord: [40.748037,-73.794906]},
        {coord: [39.3643, -74.4229]},
        { coord: [40.2206, -74.7597]},
        { coord: [38.927366, -77.031789] },
        {coord: [38.831685,-77.057211]},
        { coord: [39.290386, -76.61219] },
        { coord: [39.744431, -75.545097] },
        { coord: [39.952583, -75.165222] },
        { coord: [40.039401, -76.307078] },
        { coord: [40.602753, -75.469759] },
        { coord: [40.731507, -74.174388] },
        { coord: [40.692529, -73.990996] },
        { coord: [40.8078, -73.945801] },
        { coord: [39.925801, -75.030928] },
        { coord: [40.495921, -74.444139] },
        { coord:[39.9256,- 75.1695]},
        { coord:[40.0288,- 74.8916]}

      ] ,
      };
  },
  methods: {
    markerClick(marker) {
       bus.$emit("clickedCity", marker);
  /*   let whole = {
      coord1:  Math.round(marker.coord[0]),
      coord2: Math.round(marker.coord[1])
     }*/
   //   if(whole.coord1 == 41  && whole.coord2 == -74 || whole.coord1 == 40 && whole.coord2 == -75){
       this.center = marker.coord
       setTimeout(()=>{
         this.zoom = 10
       }, 500)
    //  }
    },
    closePanel(){
      bus.$emit("mapClicked", this.markerLatLng)
    }
  }
};
</script>

<style scoped lang="scss">
</style>
