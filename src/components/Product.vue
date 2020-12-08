<template>
  <div :key="index" class="row__items">
    <p class="row">{{ product.name }}</p>
    <p class="row">{{ product.vendor_code }}</p>
    <p class="row">{{ product.series }}</p>
    <p class="row">{{ product.price }}</p>
    <button type="button" class="table__button__edit" @click="isVisible = true; productId = index; series = product.series; show()">Edit</button>
    <ModalForEdit 
      v-if="isVisible && productId === index">
      <template #form>
        <form @submit="submit">
            <div class="edit__first__field">
              <label for="edit__first__field">Name:</label>
              <input id="edit__first__field" type="text" v-model="name">
            </div>
            <div class="edit__second__field">
              <label for="edit__second__field">Vendor Code:</label>
              <input id="edit__second__field" type="text" v-model="vendor_code">
            </div>
            <div class="modal__buttons">
              <div class="modal__button_1">
                <input  
                  class="btn__edit" 
                  type="submit"
                  value="Редактировать!">
              </div>
              <div class="modal__button_2">
                <button  @click="closeModalForEditing" class="btn__no">Назад</button>
              </div>
            </div>
          </form>
      </template>
    </ModalForEdit>
  </div>
</template>

<script>
import ModalForEdit from '../components/ModalForEdit.vue';
import gql from "graphql-tag";


const EDIT_PRODUCT = gql`
  mutation editProduct(
    $name: String!,
    $vendor_code: String!,
    $series: String!
  ) {
    update_products(
      where: {series: {_lte: $series}},
      _set: {
        name: $name,
        vendor_code: $vendor_code
      }
    ) {
      affected_rows
      returning {
        name
        vendor_code
        series
      }
    }
  }
`;
export default {
  name: 'Product',
  components: {
    ModalForEdit
  },
 props: ['product', 'index'],
 data() {
   return {
    isVisible: false,
    productId: 0,
    name: '',
    vendor_code: '',
    series: '',
   }
 },
 apollo: {},
 methods: {
   closeModalForEditing() {
     this.isVisible = false
   },
   submit() {
     
     const { name, vendor_code, series} = this.$data;
     this.$apollo.mutate({
       mutation: EDIT_PRODUCT,
       variables: {
         name,
         vendor_code,
         series
       },
       refethQueries: ["getProducts"]
     });
     this.isVisible = false;
   },
   show() {
     console.log(this.productId)
   }
 }
}
</script>


<style scoped lang="scss">
.row__items {
  display: flex;
  justify-content: space-around;
  border-bottom: 1px solid black;
  .table__button__edit {
    background-color: rgb(104, 175, 63);
    cursor: pointer;
    outline: none;
    &:hover {
      background-color: rgb(32, 78, 5);
    }
  }
  .row {
    flex-basis: 25%;
  }
}
</style>
