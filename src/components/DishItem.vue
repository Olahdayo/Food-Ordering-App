<template>
  <div class="col-md-4 mb-4">
    <div class="card">
      <img :src="dish.image" class="card-img-top" alt="dish.name" />
      <div class="card-body">
        <h5 class="card-title">{{ dish.name }}</h5>
        <p class="card-text">{{ dish.description }}</p>
        <p class="card-text">
          <strong>Price:</strong> ${{ dish.price.toFixed(2) }}
        </p>
        <input
          type="number"
          v-model.number="quantity"
          min="1"
          class="form-control mb-2"
        />
        <button class="btn btn-primary" @click="showDetails">
          View Details
        </button>
        <button class="btn btn-success ml-2" @click="addToCart">
          Add to Cart
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["dish"],
  data() {
    return {
      quantity: 1,
    };
  },
  methods: {
    showDetails() {
      this.$emit("show-details", this.dish);
    },
    addToCart() {
      if (this.quantity > 0) {
        this.$emit("add-to-cart", this.dish, this.quantity);
      }
    },
  },
};
</script>

<style scoped>
.btn-primary {
  margin-right: 10px;
}
.card-img-top {
  height: 200px;
  object-fit: cover;
}
/* Tablet view adjustments */
@media (max-width: 768px) {
  .btn-primary {
    width: 100%;
    margin-bottom: 10px;
  }
  .btn-success {
    width: 100%;
  }
}
</style>
