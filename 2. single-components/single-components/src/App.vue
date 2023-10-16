<template>

  <div class="list_src">
    Исходный список
    <div v-for="item in products" :key="item">
      {{ item }}
    </div>
  </div>

  <ListModificator v-model="products" />
</template>

<script>
import ListModificator from './components/ListModificator.vue'

export default {
  name: 'App',
  components: {
    ListModificator
  },
  data() {
    return {
      products: [{ name: "apple", price: 20 }, { name: "lemon", price: 10 }, { name: "kiwi", price: 10 }, { name: "pineapple", price: 70 }],
    }
  },
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

.list_src {
  width: fit-content;
  background: #d2c6c6;
  border: dashed #535384;
  margin-bottom: 60px;
}
</style>
