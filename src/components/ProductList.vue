<template>
  <div id="app">
    <h1>Products</h1>
    <EditModal v-if="showEdit" @close="closeEditModal" :product="this.toEditProduct"></EditModal>
    <AddModal v-if="showAdd" @close="closeAddModal" @closeDefault="closeAddModalDefault"></AddModal>

    <div class="control-panel">
      <button @click="openAddModal">Add Product</button>
      <table>
        <thead>
          <th>Name</th>
          <th>Description</th>
          <th>Price</th>
          <th>Image</th>
          <th>Action</th>
        </thead>
        <transition-group name="fade">
          <tr v-for="(product, index) in this.products" :key="product" @click="openEditModal(index, product)" class="item">
            <td>{{ product.name }}</td>
            <td>{{ product.desc }}</td>
            <td>{{ product.price }}</td>
            <td><img :src="product.image" alt="Product Image" style="width: 100px; height: auto;"></td>
            <td v-on:click.stop="">
              <button @click="deleteProduct(index)">Delete</button>
            </td>
          </tr>
        </transition-group>
      </table>
    </div>
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
        { name: "Coffee 2", desc: "Cortado", price: 110, image: "" },
        { name: "Coffee 3", desc: "Red Eye", price: 125, image: "" },
        { name: "Coffee 4", desc: " Mocha", price: 100, image: "" },
        { name: "Coffee 5", desc: "Latte", price: 140, image: "" },
      ]
    }
  },

  methods: {
    // Your existing methods here...
  }
}
</script>

<style scoped>
/* Your existing styles here... */
</style>
