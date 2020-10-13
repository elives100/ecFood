<template>
  <div>
    <h1>Top Local Restaurants</h1>
   <div v-if="restaurants.length < 1" class="description">
    <h2>Welcome <br> This site is used so you can easily access restaurants 
    across the East Coast.  Pick a city and check the top 4 star Restaurants
    based on Trip Advisory</h2>
   </div>
    
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
    };
  },
  methods: {
    onChangePage(){
      
    }
  },
  created() {
    bus.$on("clickedCity", (data) => {
      axios
        .get(
          `https://tripadvisor1.p.rapidapi.com/restaurants/list-by-latlng?limit=15&restaurant_tagcategory=10591&restaurant_mealtype=10599&currency=USD&distance=10&lunit=mi&lang=en_US&min_rating=4&latitude=${data.coord[0]}&longitude=${data.coord[1]}`,
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
          this.restaurants = array;
          console.log(this.restaurants);
        })
        .catch((err) => {
          console.log(err);
        });
    });
  },
};
</script>

<style lang="css" scoped>

h1{
  text-align: center;
  margin-top: 20px;
  margin-bottom: 20px;
  text-decoration: underline;
}

.description{
  text-align: center;
  margin: 0 20px;
  font-size: 12px;
  font-weight: bold;
  line-height: 30px;
}

</style>
