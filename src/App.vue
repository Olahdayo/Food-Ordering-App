<template>
  <div class="container d-flex">
    <div class="dish-list flex-grow-1">
      <h1 class="text-center my-4">
        Order The Best
        <span @click="toggleSearch" class="search-icon">
          <i class="fa fa-search"></i>
        </span>
      </h1>
      <input
        v-if="isSearchVisible"
        type="text"
        v-model="searchQuery"
        placeholder="Search dishes..."
        class="form-control mb-3"
      />
      <DishList
        :dishes="filteredDishes"
        @show-details="showDetails"
        @add-to-cart="addToCart"
      />
      <DishModal
        v-if="selectedDish"
        :dish="selectedDish"
        @close="selectedDish = null"
      />
    </div>
    <div class="cart-summary">
      <CartSummary
        ref="cartSummary"
        :cartItems="cartItems"
        :totalPrice="totalPrice"
        @remove-item="removeItem"
        @place-order="handlePlaceOrder"
      />
    </div>
    <OrderConfirmation
      v-if="isOrderModalVisible"
      @confirm="confirmOrder"
      @cancel="isOrderModalVisible = false"
    />
  </div>
</template>

<script>
import DishList from "./components/DishList.vue";
import CartSummary from "./components/CartSummary.vue";
import DishModal from "./components/DishModal.vue";
import OrderConfirmation from "./components/OrderConfirmation.vue";

export default {
  components: {
    DishList,
    CartSummary,
    DishModal,
    OrderConfirmation,
  },
  data() {
    return {
      dishes: [
        {
          id: 1,
          name: "Pasta",
          price: 12.99,
          description: "Delicious tasty pasta with tomato sauce",
          image: "/public/images/pasta2.jpg",
        },
        {
          id: 2,
          name: "Burger",
          price: 8.99,
          description: "Juicy burger with cheese and bacon",
          image: "/public/images/burger.jpg",
        },
        {
          id: 3,
          name: "Salad",
          price: 7.99,
          description: "Fresh mixed greens with vinaigrette",
          image: "/public/images/salad.jpg",
        },
        {
          id: 4,
          name: "Pizza",
          price: 15.99,
          description: "Cheesy pizza with pepperoni",
          image: "/public/images/pizza.jpg",
        },
        {
          id: 5,
          name: "Sushi",
          price: 18.99,
          description: "Assorted sushi platter",
          image: "/public/images/sushi.jpg",
        },
        {
          id: 6,
          name: "Steak",
          price: 22.99,
          description: "Grilled steak with garlic butter",
          image: "/public/images/steak.jpg",
        },
        {
          id: 7,
          name: "Ice Cream",
          price: 4.99,
          description: "Vanilla ice cream with chocolate sauce",
          image: "/public/images/icecream.jpg",
        },
        {
          id: 8,
          name: "Tacos",
          price: 9.99,
          description: "Soft tacos with beef and veggies sprinkles",
          image: "/public/images/tacos.jpg",
        },
        {
          id: 9,
          name: "Cream De late",
          price: 3.99,
          description: "Vanilla ice cream with chocolate sauce",
          image: "/public/images/icecream.jpg",
        },
      ],
      cartItems: [],
      selectedDish: null,
      isOrderModalVisible: false,
      isSearchVisible: false,
      searchQuery: "",
    };
  },

  methods: {
    toggleSearch() {
      this.isSearchVisible = !this.isSearchVisible;
      if (!this.isSearchVisible) this.searchQuery = ""; 
    },


    showDetails(dish) {
      this.selectedDish = dish;
    },


    addToCart(dish, quantity) {
      const existingItem = this.cartItems.find((item) => item.id === dish.id);
      if (existingItem) {
        existingItem.quantity += quantity;
      } else {
        this.cartItems.push({ ...dish, quantity });
      }
    },


    removeItem(index) {
      this.cartItems.splice(index, 1);
    },


    handlePlaceOrder() {
      console.log("Place order event received");
      this.isOrderModalVisible = true;
    },


    confirmOrder() {
      alert("Your order has been successfully placed!");
      this.cartItems = [];
      this.isOrderModalVisible = false;
      this.$refs.cartSummary.clearUserDetails();
    },
  },


  computed: {
    filteredDishes() {
      if (!this.searchQuery) return this.dishes;
      return this.dishes.filter((dish) =>
        dish.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },


    totalPrice() {
      return this.cartItems
        .reduce((sum, item) => sum + item.price * item.quantity, 0)
        .toFixed(2);
    },
  },

  
  watch: {
    "cartItems.length"(newLength) {
      if (newLength > 5) {
        alert("You have more than 5 items in your cart!");
      }
    },
  },
};
</script>

<style>
.container {
  max-width: 1200px;
  display: flex;
}

.search-icon {
  cursor: pointer;
  margin-left: 10px;
  font-size: 1.1em;
  color: #2c1061;
}

.dish-list {
  flex-grow: 2;
}

.cart-summary {
  width: 300px;
  margin-left: 50px;
}

.card {
  width: 100%;
  margin: 0 auto;
}
.col-md-4 {
min-width: 300px;
}

input[type="text"] {
  align-items: center;
  width: 250px;
  margin-top: 10px;
}
/* Tablet view adjustments */
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
  .card {
    max-width: 90%;
    flex: 1;
    margin: 10px;
  }

  .cart-summary {
    width: 100%;
    margin-left: 0;
    margin-top: 20px;
  }
}
/* Mobile view adjustments */
@media (max-width: 480px) {
  .container {
    flex-direction: column;
  }

  .dish-list {
    width: 100%;
    margin: 0;
  }

  .cart-summary {
    width: 100%;
    margin: 20px 5px;
  }

  .card {
    max-width: 97%;
  }
}
</style>
