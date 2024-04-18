<template>
  <h1>Products</h1>
  <EditModal v-if="showEdit" 
    @close="closeEditModal"
    :product="this.toEditProduct">
  </EditModal>

  <AddModal v-if="showAdd"
  @close="closeAddModal">
  </AddModal>
                      
  <button @click="openAddModal">Add Product</button>
  <table>
    <thead>
      <th>Name</th>
      <th>Description</th>
      <th>Price</th>
      <th>Action</th>
    </thead>
    <transition-group name="fade">
      <tr v-for="(product, index) in this.products" :key="product.name" @click="openEditModal(index, product)">
        <td>{{ product.name }}</td>
        <td>{{ product.desc }}</td>
        <td>{{ product.price }}</td>
        <td v-on:click.stop="">
          <button @click="deleteProduct(index)">Delete</button>
        </td>
    </tr>
    </transition-group>
  </table>

</template>

<script>
import EditModal from '../components/EditModal.vue'
import AddModal from '../components/AddModal.vue'

export default {
  name: 'ProductList',
  components:{
    EditModal,
    AddModal
  },
  data(){
    return {
      showEdit: false,
      showAdd: false,
      toEditProduct: null,
      products: [
        {name: "product 1", desc: "description 1", price: 12},
        {name: "product 2", desc: "description 2", price: 34},
        {name: "product 3", desc: "description 3", price: 87},
      ]
    }
  },

  methods:{
    addProduct(newProduct){
      this.products.push(newProduct);
      // alert("New product successfully added. ");
    },

    editProduct(product){
      let id = product.id;
      delete product.id;
      
      let index = this.products.map(e => e.name).indexOf(product.name);

      if(index != id && index != -1){
        alert("Product name for " + product.name + " is already exist");
        return;
      }
      this.products[id] = product;
      alert("Edit saved");
    },

    deleteProduct(index){
      let currentProduct = this.products[index];
      let conf = confirm("Are you sure to delete " + currentProduct.name + "?");

      if(conf){
        this.products.splice(index, 1);
      }
    },

// --------------------------- open and close modal methods --------------------------- \\
    openEditModal(index, product){
      this.showEdit = true;

      // creating product payload array with id array key with the value of index
      product.id = index;
      this.toEditProduct = product;
    },

    closeEditModal(product){
      this.showEdit = false;
      this.editProduct(product);
      
    },

    openAddModal(){
      this.showAdd = true;
    },

    closeAddModal(newProduct){
      this.showAdd = false;
      // call addProduct method
      this.addProduct(newProduct);
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0;
}

</style>
