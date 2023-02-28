<template>
  <div class="home">
    <div class="splash-container">
      <div class="splash">
        <h1>Splendid Food</h1>
      </div>
    </div>
    <main class="wrapper">
      <h1>Recommended</h1>
      <!-- Only show the first 3 items to be recommended -->
      <div class="recommended">
        <!-- Use the v-for directive to loop through the inventory object -->
        <ProductCardComponent
          v-for="(product, index) in inventory.slice(0,3)"
          :key="index"
          class="card"
          :index="index"
          :product="product"
          :addToCart="addToCart"
        />
      </div>
    </main>
  </div>
</template>

<script>
import ProductCardComponent from '@/components/ProductCardComponent.vue'

export default {
  name: 'HomeView',
  props: [
    'inventory',
    'addToCart'
  ],
  components: {
    ProductCardComponent
  }
}
</script>
