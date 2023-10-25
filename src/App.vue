<template>
  <img alt="Vue logo" src="./assets/logo.png">

  <ProductDetails v-for="item in products" :key="item.id" :nameItem="item"></ProductDetails>


</template>

<script>
import ProductDetails from './components/ProductDetails.vue'

export default {
  name: 'App',
  components: {
    ProductDetails
  },
  data () {
    return {
      products: [{
        name: 'apple',
        price: 200,
        availiable: true
      },
      {
        name: 'pineapple',
        price: 300,
        availiable: false
      },
      {
        name: 'orange',
        price: 100,
        availiable: true
      }
      ]
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
