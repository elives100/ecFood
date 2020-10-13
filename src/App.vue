<template>
  <div id="app">
 
    <div class="map">
      <spinner></spinner>
      <popup class="popup"></popup>
      <Maps></Maps>
    </div>
   

  </div>
</template>

<script>
import Maps from "./components/GoogleMap.vue";
import popup from "./components/popup.vue"
import spinner from "./components/spinner.vue"
export default {
  name: "App",
  components: {
    Maps: Maps,
    popup:popup,
    spinner: spinner
  },
  data() {
    return {
    };
  },
};
</script>

<style lang="scss" scope>
* {
  padding: 0;
  margin: 0;
}

#app {
 // display: grid;
  height: 100vh;
 // grid-template-columns: 60% 40%;
 // grid-template-areas: "left right";
}

/*.rightside {
  grid-area: right;
  max-width: 100%;
  overflow: scroll;
  
}*/

.map {
 // grid-area: left;
 // display: flex;
//  flex-direction: column;
  background-size: cover;
  background-repeat: no-repeat;
  z-index: 0;
}



</style>
