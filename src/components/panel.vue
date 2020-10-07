<template>
  <div>
    <div class="container">
      <div class="panel">
        <span class="name"> {{ name }} </span>
        <span class="address">{{ address }} </span>
        <span class="phone"> {{ phone }} </span>
        <span class="website"> {{ website }} </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    address: String,
    phone: String,
    website: String,
  },
};
</script>

<style lang="scss" scoped>
.panel {
  border: 2px solid blue;
  color: white;
  display: flex;
  flex-direction: column;
}
</style>
