<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
        <span>
          Cart
          <i class="icofont-cart-alt icofont-1x"></i>
        </span>
        <!-- Use the toggle method to close the sidebar -->
        <button @click="toggle" class="cart-close">&times;</button>
      </h1>

      <div class="cart-body">
        <table class="cart-table">
          <thead>
            <tr>
              <th><span class="sr-only">Product Image</span></th>
              <th>Product</th>
              <th>Price</th>
              <th>Qty</th>
              <th>Total</th>
              <th><span class="sr-only">Actions</span></th>
            </tr>
          </thead>
          <tbody>
            <!-- Use the v-for directive to loop through the cart object -->
            <tr v-for="(quantity, product_index, i) in cart" :key="i">
              <td class="center"><i class="icofont-{{ inventory[product_index].icon }} icofont-3x"></i></td>
              <td class="center">{{ inventory[product_index].name }}</td>
              <td class="center">${{ inventory[product_index].price.USD }}</td>
              <td class="center">{{ quantity }}</td>
              <td class="center">${{ (inventory[product_index].price.USD * quantity).toFixed(2) }}</td>
              <td class="center">
                <button @click="remove(product_index)" class="btn btn-light cart-remove">
                  &times;
                </button>
              </td>
            </tr>
          </tbody>
        </table>

        <p class="center" v-if="!Object.keys(cart).length"><em>No items in cart</em></p>
        <div class="spread">
          <!-- Remember to use the $ sign to display the total price -->
          <span><strong>Total:</strong> ${{ cartTotal }} </span>
          <button class="btn btn-light">Checkout</button>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  // "toggle" is the function that will be called when the user clicks on the close button
  props: ['toggle', 'inventory', 'cart', 'remove'],
  computed: {
    cartTotal () {
      // Calculate the total price of the cart
      // Please note that the key is the index of the item in the inventory object
      return Object.keys(this.cart).reduce((total, key) => {
        return total + this.inventory[key].price.USD * this.cart[key]
      }, 0).toFixed(2)
    }
  }
}
</script>
