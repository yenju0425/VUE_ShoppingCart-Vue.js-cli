<template>
  <div class="card">
    <div class="card-title">
      {{ product.name }}
    </div>
    <div class="card-body">
      <!-- v-bind the icon to the icofont class -->
      <i :class="iconClass"></i>
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
            <input type="number" v-model.number="quantity">
          </div>
        </div>
      </form>
    </div>
    <div class="card-footer">
      <!-- Use the addToCart method to add the item to the cart -->
      <button @click="addAndReset()" class="btn btn-light">
        Add to cart
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    'product',
    'index',
    'addToCart'
  ],
  data () {
    return {
      quantity: 0
    }
  },
  methods: {
    resetQuantity () {
      this.quantity = 0
    },
    addAndReset () {
      // add the item to the cart
      this.addToCart(this.index, this.quantity)

      // reset the quantity to 0
      this.resetQuantity()
    }
  },
  computed: {
    iconClass () {
      return `icofont-${this.product.icon} icofont-3x`
    }
  }
}
</script>
