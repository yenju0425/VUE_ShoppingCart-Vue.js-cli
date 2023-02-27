<template>
  <div class="home">
    <div class="splash-container">
      <div class="splash">
        <h1>Splendid Food</h1>
      </div>
    </div>

    <main class="wrapper">
      <h2>Recommended</h2>
      <!-- Only show the first 3 items to be recommended -->
      <div class="recommended">
        <!-- Use the v-for directive to loop through the inventory object -->
        <div v-for="(product, i) in inventory.slice(0,3)" :key="i" class="card">
          <div class="card-title">
            {{ product.name }}
          </div>
          <div class="card-body">
            <i class="icofont-10x icofont-{{ product.icon }}"></i>
            <form>
              <div class="row">
                <div class="cell">
                  <label>Type:</label>
                </div>
                <div class="cell">
                  <em>{{ product.type }}</em>
                </div>
              </div>
              <div class="row">
                <div class="cell">
                  <label>Price:</label>
                </div>
                <div class="cell">
                  ${{ product.price.USD }}
                </div>
              </div>
              <div class="row">
                <div class="cell">
                  <label>Quantity:</label>
                </div>
                <div class="cell">
                  <!-- Use the v-model.number directive to make sure the value is a number -->
                  <!-- Though the quantity is not currently existing in the data object, it will be added as needed -->
                  <input type="number" v-model.number="product.quantity">
                </div>
              </div>
            </form>
          </div>
          <div class="card-footer">
            <!-- Use the addToCart method to add the item to the cart -->
            <button @click="addToCart(i)" class="btn btn-light">
              Add to cart
            </button>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import food from '../food.json'

export default {
  name: 'HomeView',
  data () {
    return {
      inventory: food
    }
  },
  components: {
  }
}
</script>
