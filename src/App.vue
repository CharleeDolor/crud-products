<template>
  <div id="app">
    <ProductList />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';

export default {
  name: 'App',
  components: {
    ProductList
  }
};
</script>

<<<<<<< HEAD
=======
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff; /* White text color */
  margin-top: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 5rem;
  background-color: #394867; /* Background color */
  padding: 20px; /* Padding for better readability */
}

table, th, td {
  border: 1px solid #ffffff; /* White borders */
  border-collapse: collapse;
  color: #ffffff; /* White text color */
}

td, th {
  padding: 0.5rem;
}

.modal-group {
  margin: 1rem;
  display: flex;
  flex-direction: column;
  align-items: start;
}
</style>
>>>>>>> ab00b9c6a3939a6159480c9c3af34cb546e28cca
