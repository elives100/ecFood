<template>
  <div class="mapContainer">
    <button @click="pickLocation" class="pickButton">Pick City</button>
    <div v-if="pickContainer" class="search">
      <div class="statWrapper">
        <div class="states">
          <h1>Pick a State</h1>
          <ul v-for="(states, index) in nonRepeatedState" :key="index">
            <li>
              <button @click="stateClicked(states)">{{states}}</button>
            </li>
          </ul>
        </div>
        <div class="city">
          <h1>Pick a City</h1>
          <ul v-for="(citySelect,index) in cityGroup" :key="index">
            <li>
              <button @click="markerClick(marker,citySelect)">{{ citySelect.city }}</button>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <l-map
      class="actualMap"
      @click="closePanel()"
      :options="{ scrollWheelZoom: false }"
      style="height: 100vh"
      :zoom="zoom"
      :center="center"
    >
      <l-tile-layer :url="url"></l-tile-layer>
      <div v-for="(marker, index) in markerLatLng" :key="index">
        <l-marker @click="markerClick(marker,city)" :lat-lng="marker.coord"></l-marker>
      </div>
    </l-map>
  </div>
</template>

<script>
import { bus } from "../main.js";
import dataArray from "../data.js";
export default {
  props: {
    zoomPort: Number,
    centerPort: Array
  },
  data() {
    return {
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      zoom: this.zoomPort,
      center: this.centerPort,
      pickContainer: false,
      markerLatLng: dataArray,
      pickState: true,
      newStateValue: "undefined",
      cityShow: false
    };
  },
  methods: {
    markerClick(marker, city) {
      if (marker) {
        console.log(marker.coord);
        this.pickContainer = false;
        bus.$emit("clickedCity", marker);
        this.center = marker.coord;
        setTimeout(() => {
          this.zoom = 10;
        }, 500);
      } else {
        console.log(city.coord);
        this.pickContainer = false;
        bus.$emit("clickedCity", city);
        this.center = city.coord;
        setTimeout(() => {
          this.zoom = 10;
        }, 500);
      }
    },
    /*  cityClicked(city) {
    
    },*/
    closePanel() {
      bus.$emit("mapClicked", this.markerLatLng);
      this.zoom = 7;
      this.center = [39.988757, -76.24702];
    },
    pickLocation() {
      this.pickContainer = !this.pickContainer;
    },
    stateClicked(states) {
      this.newStateValue = states;
      this.cityShow = !this.cityShow;
      console.log(this.newStateValue);
    }
  },
  computed: {
    nonRepeatedState() {
      const stateOnly = this.markerLatLng.map(item => item.state);

      const noDuplicate = stateOnly.filter((value, index) => {
        return stateOnly.indexOf(value) === index;
      });
      return noDuplicate;
    },
    cityGroup() {
      const filterObjects = this.markerLatLng.filter(theObject => {
        if (theObject.state == this.newStateValue) return theObject;
      });
      return filterObjects.map(e => {
        return e;
      });
    }
  }
};
</script>

<style scoped lang="scss">
::-webkit-scrollbar {
  background: transparent;
}

.states {
  width: 50%;
  border-radius: 25px;
  overflow: scroll;
  overflow-x: hidden;
}
.city {
  width: 50%;
  border-radius: 25px;
  overflow: scroll;
  overflow-x: hidden;
}
.statWrapper {
  display: flex;
  flex-direction: row;
  overflow: hidden;
}
.search {
  height: 50%;
  width: 45%;
  background-color: rgba(8, 30, 48, 0.842);
  position: absolute;
  right: 1px;
  bottom: 10px;
  z-index: 500;
  color: wheat;
  padding: 20px;
  display: flex;
  flex-direction: column;
  border-radius: 25px;
}

ul {
  list-style: none;
  display: flex;
  justify-content: center;
}

li {
  line-height: 70px;
}

button {
  width: 100px;
  height: 60px;
  border-radius: 25px;
  border: none;
  background-image: linear-gradient(to bottom right, #80878d, #1b344e);
  color: wheat;
  padding: 5px;
}

.pickButton {
  position: absolute;
  z-index: 999;
  right: 1px;
  color: white;
  font-weight: bold;
}

h1 {
  text-decoration: underline;
  text-align: center;
  margin-bottom: 15px;
}

@media (max-width: 576px) {
  .search {
    background-color: rgba(8, 30, 48, 0.842);
    width: 80%;
  }
  h1 {
    font-size: 20px;
  }
}
</style>
