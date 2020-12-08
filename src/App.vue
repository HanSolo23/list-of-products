<template>
  <div id="app">
    <ProductsList/>
  </div>
</template>

<script>
import ProductsList from './components/ProductsList.vue'

export default {
  name: 'App',
  components: {
    ProductsList
  }
}
</script>

<style lang="scss">
body {
  background-color: rgb(56, 130, 148);
}
</style>
