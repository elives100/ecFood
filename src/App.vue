<template>
  <div id="app">
    <div class="map">
      <transition name="fade">
        <div v-if="intro" class="shadow">
          <h4>&#40;Trip Advisor&#41;</h4>
          <h1>Top Ranked Restaurants</h1>
          <h3>In the East</h3>
          <button @click="intro = false">Explore</button>
        </div>
      </transition>
      <spinner></spinner>
      <popup class="popup"></popup>
      <v-show-at no-match
        ><Maps :centerPort="[39.988757, -76.24702]" :zoomPort="7"></Maps
      ></v-show-at>
      <v-show-at small
        ><Maps :centerPort="[39.988757, -76.24702]" :zoomPort="7"></Maps
      ></v-show-at>
      <v-show-at medium
        ><Maps :centerPort="[39.988757, -76.24702]" :zoomPort="7"></Maps
      ></v-show-at>
      <v-show-at large
        ><Maps :centerPort="[39.988757, -75.24702]" :zoomPort="8"></Maps
      ></v-show-at>
      <v-show-at xlarge
        ><Maps :centerPort="[39.988757, -75.24702]" :zoomPort="8"></Maps
      ></v-show-at>
    </div>
  </div>
</template>

<script>
import Maps from "./components/GoogleMap.vue";
import popup from "./components/popup.vue";
import spinner from "./components/spinner.vue";
import { VShowAt } from "vue-breakpoint-component";

export default {
  name: "App",
  components: {
    Maps: Maps,
    popup: popup,
    spinner: spinner,
    VShowAt,
  },
  data() {
    return {
      intro: true,
    };
  },
};
</script>

<style lang="scss" scope>
@import url("https://fonts.googleapis.com/css2?family=Source+Serif+Pro:wght@700&display=swap");
* {
  padding: 0;
  margin: 0;
}

#app {
  height: 100v;
}

.map {
  background-size: cover;
  background-repeat: no-repeat;
  z-index: 0;
}

.shadow {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.733);
  z-index: 9999;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: wheat;
  letter-spacing: 5px;
  font-family: "Source Serif Pro", serif;
  h3 {
    margin: 30px 30px;
  }
  h1 {
    text-align: center;
  }
  button {
    width: 130px;
    height: 60px;
    border-radius: 25px 5px;
    border: none;
    background-image: linear-gradient(to bottom right, #bdc3c7, #2c3e50);
    color: wheat;
    font-family: "Source Serif Pro", serif;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s;
}

.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
