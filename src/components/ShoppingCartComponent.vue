<template>
  <div class="shopping_cart">
    <div class="mk_container">
      <div class="py-2 fs-3 text-end" @click="store.openCart = !store.openCart">
        <i class="fa-solid fa-circle-xmark"></i>
      </div>
      <h6>Shopping Cart</h6>
      <div class="product_list mt-5">
        <div class="cart_item d-flex py-3 justify-content-between align-items-center"
          v-for="(cartItem, index) in store.cartData" :key="index">
          <div>
            <p>{{ cartItem.name }}</p>
            <p>{{ cartItem.price_sign }}{{ cartItem.price }}</p>
            <input type="number" class="w-25 me-2" v-model="cartItem.quantity" min="1"/>
            <label for="quantity">Quantity</label>
          </div>
          <span @click="removeFromCart()"><i class="fa-solid fa-trash"></i></span>
        </div>
      </div>
      <div class="cart_total mt-4 d-flex justify-content-between me-auto">
        <span class="fs-4">Total:</span>
        <span class="fs-4">{{ this.cartTotal.toFixed(2) }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { store } from "../store";
export default {
  name: "CartComponent",
  data() {
    return {
      store  
    };
  },
  methods: {
    removeFromCart(index) {
      store.cartData.splice(index, 1);
      localStorage.setItem(`cart`, JSON.stringify(store.cartData));
    },
  },
  computed: {
    cartTotal() {
      return store.cartData.reduce((a, b) => a + b.price * b.quantity, 0);
    },
  },
  mounted() {
    
  }
};
</script>

<style lang="scss" scoped>
@use "../assets/styles/partials/variables" as *;
@use "../assets/styles/partials/mixins" as *;

.product_list {
  overflow-y: auto;
  height: 70vh;
}

.cart_item {
  border-bottom: 1px solid black;
}

.shopping_cart {
  position: fixed;
  top: 0;
  right: 0;
  width: 500px;
  min-height: 100vh;
  background-color: $mk_white;
  box-shadow: -1px 1px 10px 0px $mk_txt_light_gray;
  z-index: 20;
  color: $mk_txt_dark_gray;

  i {
    cursor: pointer;
  }
}
</style>
