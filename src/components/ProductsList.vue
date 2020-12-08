<template>
  <div class="table">
    <div class="title">
      <p>Name</p>
      <p>Vendor Code</p>
      <p>Series</p>
      <p>Price</p>
    </div>
    <div class="product">
      <Product 
        v-for="(product, index) in paginatedProducts" 
        :key="index" :product="product" 
        :index="index">
      </Product>
    </div>
    <div class="pagination">
      <div 
        class="page" 
        v-for="page in pages" 
        :key="page" 
        @click="nextPage(page)" 
        :class="{ active: page === pageNumber }">
        {{ page }}
      </div>
    </div>
  </div>
</template>

<script>
import Product from '../components/Product.vue';
import gql from "graphql-tag";

const GET_PRODUCTS = gql`
  query getProducts {
    products {
      name
      vendor_code
      series

    }
  }
`;

export default {
  name: 'ProductsList',
  components: {
    Product
  },
  data() {
    return {
      productsPerPage: 40,
      pageNumber: 1,
      products: []
    }
  },
  apollo: {
    products: {
      query: GET_PRODUCTS
    }
  },
  computed: {
    pages() {
      return Math.ceil(this.products.length / 10);
    },
    paginatedProducts() {
      let from = (this.pageNumber - 1) * this.productsPerPage;
      let to = from + this.productsPerPage;
      return this.products.slice(from, to);
    }
  },
  methods: {
    nextPage(page) {
      this.pageNumber = page;
    }
  }
}
</script>


<style scoped lang="scss">
.table {
  display: flex;
  flex-direction: column;
  max-width: 1500px;
  margin: 100px auto;
  border: 1px solid black;
  padding: 10px;
  background-color: rgb(96, 150, 120);
  box-shadow: 2px 2px 10px 1px;
  font-family: sans-serif;
  .title {
    display: flex;
    justify-content: space-around;
    border-bottom: 1px solid black;
    p {
      flex-basis: 25%;
    }
  }
  .product {
    margin-bottom: 10px;
  }
  .pagination {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    .page {
      border: 1px solid black;
      padding: 10px;
      width: 40px;
      margin: 5px;
      text-align: center;
      cursor: pointer;
      &:hover {
        background-color: rgb(97, 92, 92);
      }
    }
    .active {
      background-color: rgb(97, 92, 92);
    }
  }
}

</style>
