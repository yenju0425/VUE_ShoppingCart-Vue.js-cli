<template>
  <main class="wrapper">
    <h1>Products</h1>
    <div class="card-container">
      <!-- Use the v-for directive to loop through the inventory object -->
      <ProductCardComponent
        v-for="(product, index) in inventory"
        :key="index"
        class="card"
        :index="index"
        :product="product"
        :addToCart="addToCart"
      />
    </div>
  </main>
</template>

<script>
import ProductCardComponent from '@/components/ProductCardComponent.vue'

export default {
  props: [
    'inventory',
    'addToCart'
  ],
  components: {
    ProductCardComponent
  }
}
</script>
