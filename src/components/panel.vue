<template>
  <div>
      <div class="panel">
        <div class="panelTitle">
          <img :src="photo.images.small.url"/>
          </div>
        <div class="panelBody">
        <span class="name"> <a target="_blank" :href="website">{{ name }} </a> </span><br>
        <span class="address">{{ address }} </span><br>
        <span class="phone"> {{ phone }} </span><br>
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
    photo: Object
  },
};
</script>

<style lang="scss" scoped>

.panel{
  border-radius: 25px;
  color:wheat;
  text-align: center;
  padding: 5px;
}

.panelBody{
  display: flex;
  flex-direction: column;
}

a{
  color: wheat;
  font-size:20px;
}

 h1{
   text-decoration: underline;
   font-size: 20px;
 }

 img{
   width: 120px;
   height: 100px;
 }

 @media (max-width: 767.98px) { 
   img{
     width: 90px;
     height: 90px;
   }
   h1{
     font-size: 16px;
   }
   .panelBody{
     font-size: 12px;
   }
  }
</style>
