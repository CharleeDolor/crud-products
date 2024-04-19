<template>
   <img :src="require('@/assets/kapelogo.png')" alt="Coffee Shop Logo" class="imglog">

  <EditModal v-if="showEdit" @close="closeEditModal" @closeDefault="closeEditModalDefault" :product="toEditProduct" />
  <AddModal v-if="showAdd" @close="closeAddModal" @closeDefault="closeAddModalDefault" />

  <div class="control-panel">
    <button @click="openAddModal" class="add-btn">Add Product</button>
    <table v-if="this.products.length > 0">
      <thead>
        <th>Name</th>
        <th>Description</th>
        <th>Price</th>
        <th>Action</th>
      </thead>
      <transition-group name="slide">
        <tr v-for="(product, index) in products" :key="product" @click="openEditModal(index, product)" class="item"
          v-bind:class="{ 'slide-enter-active': product.animate }">
          <td>{{ product.name }}</td>
          <td>{{ product.desc }}</td>
          <td>{{ product.price }}</td>
          <td v-on:click.stop="">
            <button @click="deleteProduct(product, index)" class="del-btn"></button>
          </td>
        </tr>
      </transition-group>
    </table>
    <h2 v-else style="align-self: center;">Empty</h2>
  </div>
</template>

<script>
import EditModal from '../components/EditModal.vue'
import AddModal from '../components/AddModal.vue'

export default {
  name: 'ProductList',
  components: {
    EditModal,
    AddModal
  },
  data() {
    return {
      showEdit: false,
      showAdd: false,
      toEditProduct: null,
      products: [
        { name: "Coffee 1", desc: "Cappuccino ", price: 120, image: "" },
        // { name: "Coffee 2", desc: "Cortado", price: 110, image: "" },
        // { name: "Coffee 3", desc: "Red Eye", price: 125, image: "" },
        // { name: "Coffee 4", desc: " Mocha", price: 100, image: "" },
        // { name: "Coffee 5", desc: "Latte", price: 140, image: "" },
      ]
    }
  },

  methods: {
    // Your existing methods here...
    addProduct(newProduct) {

      // check if new product name is already existing
      let pos = this.products.findIndex(i => i.name.toLowerCase() == newProduct.name.toLowerCase());
      if (pos > -1) {
        alert(newProduct.name + " already exists.");
        return;
      }

      // Add animation flag to the new product
      newProduct.animate = true;

      // Push the new product into the products array
      this.products.push(newProduct);
    },

    editProduct(product) {
      let id = product.id;
      delete product.id;

      // VALIDATIONS
      // check for duplicate product name by getting the index of product name
      var pos = this.products.findIndex(i => i.name.toLowerCase() === product.name.toLowerCase());

      // if pos value is not equal to -1, this means that this product name already exist
      if (pos != -1 && pos != id) {
        alert("Cannot rename to " + product.name + ". It is already existing.");
        return;
      }

      let index = this.products.map(e => e.name).indexOf(product.name);

      if (index != id && index != -1) {
        alert("Product name for " + product.name + " is already exist");
        return;
      }
      this.products[id] = product;
      alert("Edit saved");
    },

    deleteProduct(product, index) {
      let currentProduct = this.products[index];
      let conf = confirm("Are you sure to delete " + currentProduct.name + "?");

      if (conf) {
        this.products.splice(index, 1);
        alert("Product " + product.name + " is removed");
      }
    },

    // --------------------------- open and close modal methods --------------------------- \\
    openEditModal(index, product) {
      this.showEdit = true;

      // creating product payload array with id array key with the value of index
      product.id = index;
      this.toEditProduct = product;
    },

    closeEditModal(product) {
      this.showEdit = false;
      this.editProduct(product);

    },

    openAddModal() {
      this.showAdd = true;
    },

    closeAddModal(newProduct) {
      this.showAdd = false;
      // call addProduct method
      this.addProduct(newProduct);

    },

    closeAddModalDefault() {
      this.showAdd = false;
    },

    closeEditModalDefault() {
      this.showEdit = false;
    }
  }
}
</script>

<style scoped>
.slide-enter-active,
.slide-leave-active {
  transition: transform 1s ease;
}

.slide-enter-from {
  transform: translate(100%, 0);
}

.slide-leave-to{
  transform: translate(-100%, 0);
}
.imglog{
  height: 300px;
  margin-top: -100px;
}
</style>
