<template>
  <div>
    <h1>Top Local Restaurants</h1>
    <div
      class="restaurantContainer"
      v-for="(restaurant, index) in restaurants"
      :key="index"
    >
      <panel
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
  methods: {},
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

<style lang="css" scoped></style>
