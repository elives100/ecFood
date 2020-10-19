<template>
  <div>
    <div v-if="loading" class="container">
      <div class="lds-ripple">
        <div></div>
        <div></div>
      </div>
    </div>
    <div v-else>{{error}}</div>
  </div>
</template>


<script>
import { bus } from "../main.js";

export default {
  data() {
    return {
      loading: false,
      error: ""
    };
  },
  created() {
    bus.$on("clickedCity", () => {
      this.loading = true;
      console.log(this.loading);
    });
    bus.$on("testing", () => {
      this.loading = false;
      console.log(this.loading);
    });
    bus.$on("mapError", data => {
      this.loading = false;
      this.error = data;
    });
  }
};
</script>

<style scoped lang="scss">
.container {
  background-color: rgba(0, 0, 0, 0.2);
  position: absolute;
  z-index: 999;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.lds-ripple {
  display: inline-block;
  position: relative;
  width: 100px;
  height: 100px;
}
.lds-ripple div {
  position: absolute;
  border: 15px solid black;
  opacity: 1;
  border-radius: 50%;
  animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
}
.lds-ripple div:nth-child(2) {
  animation-delay: -0.5s;
}
@keyframes lds-ripple {
  0% {
    top: 36px;
    left: 36px;
    width: 0;
    height: 0;
    opacity: 1;
  }
  100% {
    top: 0px;
    left: 0px;
    width: 72px;
    height: 72px;
    opacity: 0;
  }
}
</style>