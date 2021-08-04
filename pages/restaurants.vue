<template>
  <main class="container restaurant">
    <div class="restaurantheading">
      <h1>Restaurants</h1>

      <AppSelect @change="selectedRestaurant = $event" />
    </div>
    <AppRestaurantInfo :data-source="filteredRestaurants" />
  </main>
</template>

<script>
import AppRestaurantInfo from "@/components/AppRestaurantInfo.vue";
import AppSelect from "@/components/AppSelect.vue";
import { mapState } from "vuex";

export default {
  components: {
    AppSelect,
    AppRestaurantInfo
  },
  data() {
    return {
      selectedRestaurant: ""
    };
  },
  computed: {
    ...mapState(["foodData"]),
    filteredRestaurants() {
      if (this.selectedRestaurant) {
        return this.foodData.filter(el => {
          let name = el.name.toLowerCase();
          return name.includes(this.selectedRestaurant);
        });
      }
      return this.foodData;
    }
  }
};
</script>

<style lang="scss" scoped></style>
