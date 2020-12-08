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
// @font-face {
//   font-family: 'Montserrat';
//   src: url('~@/assets/fonts/Montserrat-Regular.ttf') format('ttf'),
// }

body {
  background-color: rgb(56, 130, 148);
  
}
</style>
