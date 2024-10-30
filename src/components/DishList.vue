<template>
  <div class="row">
    <DishItem
      v-for="dish in dishes"
      :key="dish.id"
      :dish="dish"
      @show-details="showDetails"
      @add-to-cart="addToCart"
    />
  </div>
</template>

<script>
import DishItem from "./DishItem.vue";

export default {
  components: { DishItem },
  props: ["dishes"],
  methods: {
    showDetails(dish) {
      this.$emit("show-details", dish);
    },
    addToCart(dish, quantity) {
      this.$emit("add-to-cart", dish, quantity);
    },
  },
};
</script>
