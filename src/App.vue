<template>
  <div id="app">
    <div class="rightside">
      <rightSide></rightSide>
    </div>
    <div class="left">
      <Maps></Maps>
    </div>

    <component class="content" :is="component"></component>
  </div>
</template>

<script>
import Maps from "./components/GoogleMap.vue";
import rightSide from "./components/rightside";

export default {
  name: "App",
  components: {
    Maps: Maps,
    rightSide: rightSide,
  },
  data() {
    return {
      component: "",
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
  display: grid;
  height: 100vh;
  grid-template-columns: 65% 35%;
  grid-template-areas: "left right";
}

.rightside {
  grid-area: right;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(0, 0, 0, 0.986);
  color: white;
}

.left {
  grid-area: left;
  display: flex;
  flex-direction: column;
  color: white;
  background-image: linear-gradient(
    rgba(0, 0, 0, 0.842),
    rgba(0, 0, 0, 0.972),
    rgba(0, 0, 0, 0.842)
  );
  background-size: cover;
  background-repeat: no-repeat;
  .heroTitle {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: white;
    margin-top: 10%;
  }
  .content {
    padding: 5%;
    flex: 1;
  }
}
</style>
