<template>
  <div class="list-items">
    <div class="list-items__title">
      Список товаров
    </div>
    <ProductDetails v-for="item in products" :key="item.id" :product="item">{{ item.name }}</ProductDetails>
  </div>
</template>

<script>
import ProductDetails from './components/ProductDetails.vue'

import productsData from '@/data/products.txt'

export default {
  name: 'App',
  components: {
    ProductDetails
  },
  data () {
    return {
      products: JSON.parse(productsData)
    }
  }
}

</script>

<style lang="scss" >
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.list-items {
  width: fit-content;
  max-width: 600px;

  background: radial-gradient(at center, #badfa2, #c0a7ba);
  border: solid black;
  padding: 20px 20px 20px 20px;
  font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  font-weight: 800;

  &__title {
    margin-bottom: 20px;
  }
}
</style>
