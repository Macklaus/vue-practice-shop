<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-7">
          <div class="row">
            <div :key="prod.id" class="col-md-6" v-for="prod in products">
              <product v-on:add-to-cart="addToCart($event)" :product="prod" :isAlreadyInCart="productIsInCart(prod)"></product>
            </div>
          </div>
        </div>
        <div class="col-md-5 my-5">
          <cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)" :items="cart"></cart>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import products from '@/products.json';
import Product from '@/components/Product.vue';
import Cart from '@/components/Cart.vue';

export default {
  name: 'app',
  components: {
    Product,
    Cart
  },
  data(){
    return {
      products,
      cart: []
    }
  },
  methods: {
    addToCart(event){
      this.cart.push(event);
    },
    productIsInCart(product){
      let item = this.cart.find(p => p.id === product.id);
      if(item){
        return true;
      }
      return false;
    },
    removeFromCart(event){
      this.cart = this.cart.filter(product => product.id !== event.id);
    },
    pay(){
      this.cart = [];
      alert('Payment successfully');
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body{
  background-color: #FBF8F3;
}
</style>
