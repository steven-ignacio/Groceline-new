<template>
  <div class="cart">
    <div style="position:sticky; top: 0; background-color: peachpuff; opacity: 0.8;
    display: flex; align-items: center; justify-content: center;">
      <h2 v-if="this.cart.length == 0">Your cart is empty.</h2>
      <h2 v-else-if="this.cart.length == 1">You have 1 item in your cart.</h2>
      <h2 v-else>You have {{ this.cart.length }} items in your cart.</h2>
      <button class="close-btn" @click="closeCart()" style="align-self: right"><i class="fa-solid fa-xmark"></i></button>
    </div>
      <table v-if="this.cart.length > 0">
          <thead>
            <tr>
                <td>Image</td>
                <td>Item</td>
                <td>Quantity</td>
                <td>Price</td>
                <td>Total</td>
                <td></td>
            </tr>
          </thead>
          <tbody>
              <tr v-for="item in this.cart" :key="item.id">
                  <td><img :src="item.img" height="100px" width="100px"/></td>
                  <td>{{ item.name }}</td>
                  <td>
                    <button class="cart-btn" @click="item.quantity--">-</button>
                    <input type="number" v-model="item.quantity" title="Quantity" min="0"
                    style="font-size: 1.1rem; max-width: 20%; text-align: center; border-radius: 5px; border: 2px solid #93C47D">
                    <button class="cart-btn" @click="item.quantity++">+</button>
                  </td>
                  <td>₱{{ item.price }}</td>
                  <td>₱{{ item.quantity * item.price }}</td>
                  <td><button class="close-btn" @click="removeItem(item.id)" style="margin: 0; height: 40px; width: 40px; cursor: pointer;"><i class="fa-solid fa-trash"></i></button></td>
              </tr>
              <tr style="position: sticky; bottom: 0">
                <td colspan="4"></td>
                <td>₱1800</td>
                <td></td>
              </tr>
          </tbody>
      </table>
      <div style="position:sticky; bottom: 0; background-color: peachpuff; opacity: 0.8;
      display: flex; align-items: center; justify-content: center;">
        <button style="margin: 25px">Checkout</button>
      </div>
    </div>
  </template>

<script>

export default ({
  props: ['cart'],
  data() {
    return{
    }
  },
  methods: {
    closeCart(){
      // in App.vue, triggers the Cart component to run the hideCart() method
      this.$emit('closeCart')
    },
    removeItem(id){
      // in App.vue, triggers the Cart component to run the
      if(confirm('Are you sure you want to remove this item?')) {this.$emit('removeItem', id)}
    }
  },
})
</script>

<style>
table, td, tr {
  border: 1px solid #93C47D;
}

td, table {
    background-color: rgb(255, 255, 202);
}
</style>
