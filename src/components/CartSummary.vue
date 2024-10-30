<template>
  <div class="mt-4">
    <h4>Your Cart</h4>
    <ul class="list-group mb-2">
      <li
        class="list-group-item"
        v-for="(item, index) in cartItems"
        :key="item.id"
      >
        {{ item.name }} - ${{ item.price.toFixed(2) }} x {{ item.quantity }} =
        ${{ (item.price * item.quantity).toFixed(2) }}
        <button
          class="btn btn-danger btn-sm float-right"
          @click="$emit('remove-item', index)"
        >
          Remove
        </button>
      </li>
    </ul>
    <p>Total: ${{ totalPrice }}</p>
    <p>Provide Your Details</p>
    <input
      type="text"
      v-model="name"
      placeholder="Enter your name"
      class="form-control mb-2"
    />
    <input
      type="text"
      v-model="address"
      placeholder="Enter your address"
      class="form-control mb-2"
    />
    <button
      class="btn btn-primary"
      @click="placeOrder"
      :disabled="!name || !address || cartItems.length === 0"
    >
      Place Order
    </button>
  </div>
</template>

<script>
export default {
  props: ["cartItems", "totalPrice"],
  data() {
    return {
      name: "",
      address: "",
    };
  },
  methods: {
    placeOrder() {
      console.log(
        "Placing order with name:",
        this.name,
        "and address:",
        this.address
      );
      this.$emit("place-order");
    },
    clearUserDetails() {
      this.name = "";
      this.address = "";
    },
  },
};
</script>
