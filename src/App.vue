<!-- App.vue can view as the main component of the application. It handles what pages are shown and what components are shown on each page. -->

<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <!-- The Home page -->
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>

      <!-- The Products page -->
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>

      <!-- The Past Orders page -->
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>

    <!-- The Cart page -->
    <div @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity }})</span>
    </div>
  </header>

  <!-- The router-view component is where the pages are shown -->
  <router-view :inventory="inventory" :addToCart="addToCart" />

  <Sidebar
    v-if="showSidebar"
    :toggle="toggleSidebar"
    :inventory="inventory"
    :cart="cart"
    :remove="removeItem"
  />
</template>

<script>
import SidebarComponent from '@/components/SidebarComponent.vue'
import food from '@/food.json'

export default {
  components: {
    Sidebar: SidebarComponent
  },
  data () {
    return {
      showSidebar: false,
      inventory: food,
      cart: {}
    }
  },
  methods: {
    // Add the quantity of a product to the cart
    addToCart (index, quantity) {
      // Set the cart to 0 if it doesn't exist
      if (!this.cart[index]) {
        this.cart[index] = 0
      }

      // Add whatever is in the inventory to the cart, based on the type
      this.cart[index] += quantity

      console.log(this.cart)
    },

    // Toggle the sidebar
    toggleSidebar () {
      console.log(this.showSidebar)
      this.showSidebar = !this.showSidebar
    },

    removeItem (index) {
      // Remove the item from the cart
      // Please note that the key is the index of the item in the inventory object
      delete this.cart[index]
    }
  },
  computed: {
    // Calculate the total quantity of items in the cart
    totalQuantity () {
      return Object.values(this.cart).reduce((total, quantity) => {
        return total + quantity
      }, 0)
    }
  }
}
</script>
