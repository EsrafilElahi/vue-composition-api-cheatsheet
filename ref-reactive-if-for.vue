<template>
  <div>
    <h1>Shopping Cart</h1>
    <div v-if="cart.length === 0">Your cart is empty</div>
    <div v-else>
      <ul>
        <li v-for="(item, index) in cart" :key="index">
          {{ item.name }} - ${{ item.price }}
          <button @click="removeFromCart(index)">Remove</button>
        </li>
      </ul>
      <p>Total: ${{ totalPrice }}</p>
    </div>
    <hr>
    {{ msg }}
    <h2>Available Products</h2>
    <ul>
      <li v-for="(product, index) in products" :key="index">
        {{ product.name }} - ${{ product.price }}
        <button @click="addToCart(product)">Add to Cart</button>
      </li>
    </ul>
  </div>
</template>
  
<script>
import { reactive, computed } from 'vue';

export default {
  setup() {
    // Define reactive state for cart and products
    const msg = ref('test msg');

    const state = reactive({
      cart: [],
      products: [
        { id: 1, name: 'Product 1', price: 10 },
        { id: 2, name: 'Product 2', price: 20 },
        { id: 3, name: 'Product 3', price: 15 }
      ]
    });

    // Compute total price of items in cart
    const totalPrice = computed(() => {
      return state.cart.reduce((total, item) => total + item.price, 0);
    });

    // Add product to cart
    const addToCart = (product) => {
      state.cart.push(product);
    };

    // Remove product from cart
    const removeFromCart = (index) => {
      state.cart.splice(index, 1);
    };

    return {
      cart: state.cart,
      products: state.products,
      totalPrice,
      addToCart,
      removeFromCart
    };
  }
};
</script>
  