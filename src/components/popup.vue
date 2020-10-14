<template>
    <div>
    <div v-if="restaurants.length > 0" class="container">
      <button class="close" @click="closeMap()">&times;</button>
        <h1>Top Local Restaurants <br> TripAdvisor ratings</h1>
    <div
      class="restaurantContainer"
      v-for="(restaurant, index) in restaurants"
      :key="index"
    >
     <panel
        :photo="restaurant.photo"
        :name="restaurant.name"
        :address="restaurant.address"
        :phone="restaurant.phone"
        :website="restaurant.website"
      ></panel>
    </div>
        </div>
    </div>
</template>

<script>
import { bus } from "../main.js";
import axios from "axios";
import panel from "./panel";
export default {
    components: {
    panel,
  },
  data() {
    return {
      restaurants: [],
      loading: false
    };
  },
  methods: {
    closeMap(){
      this.restaurants.splice(0, this.restaurants.length)
      console.log(this.restaurants)
    }
  },
  created() {
    bus.$on("clickedCity", (data) => {
     axios
        .get(
          `https://tripadvisor1.p.rapidapi.com/restaurants/list-by-latlng?limit=20&restaurant_tagcategory=10591&restaurant_mealtype=10599&currency=USD&distance=20&lunit=mi&lang=en_US&min_rating=4&latitude=${data.coord[0]}&longitude=${data.coord[1]}`,
          {
            headers: {
              "x-rapidapi-host": "tripadvisor1.p.rapidapi.com",
              "x-rapidapi-key":
                "957a8b212bmsh70bb7e09ae2f6bbp1993cejsnab632fe079bc",
            },
          }
        )
        .then((response) => {
          let array = response.data.data;
          let value = undefined;
          let results = array.filter((item)=>{
            return item.photo !== value
          })
          this.restaurants = results;
          bus.$emit('testing', this.loading)
        })
        .catch((err) => {
          console.log(err);
        });
    });
    bus.$on("mapClicked", ()=>{
      this.restaurants.splice(0, this.restaurants.length)
      console.log(this.restaurants)
    })
  },
};

</script>

<style scoped>

.container{
  height: 90%;
  width: 60%;
  max-width: 60%;
  background-color:rgba(8, 30, 48, .9);
  z-index:999;
  position: absolute;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
  border-radius: 25px;
  text-align: center;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  overflow: scroll;
  padding-top: 20px;
}

h1{
  color: wheat;
  text-align: center;
  font-size: 30px;
  line-height: 40px;
}

.close{
  height: 30px;
  width: 30px;
  position: fixed;
  border-radius: 10px;
  z-index: 1001;
  cursor: pointer;
}
</style>