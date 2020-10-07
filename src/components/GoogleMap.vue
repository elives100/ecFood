<template>
  <div>
    <l-map style="height: 100vh" :zoom="zoom" :center="center">
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
      center: [40.145289, -74.724426],
      markerLatLng: [
        { coord: [38.892059, -77.019913] },
        { coord: [39.290386, -76.61219] },
        { coord: [39.744431, -75.545097] },
        { coord: [39.952583, -75.165222] },
        { coord: [40.039401, -76.307078] },
        { coord: [40.602753, -75.469759] },
        { coord: [40.731507, -74.174388] },
        { coord: [40.692529, -73.990996] },
        { coord: [40.8078, -73.945801] },
        { coord: [39.925801, -75.030928] },
        { coord: [40.495921, -74.444139] }
      ]
    };
  },
  computed: {},
  methods: {
    markerClick(marker) {
      bus.$emit("clickedCity", marker);
    }
  }
};
</script>

<style scoped lang="scss">
.test {
  background-color: white;
  height: 300px;
}
</style>
