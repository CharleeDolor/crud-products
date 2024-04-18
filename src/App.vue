<template>
  <ProductList/>
</template>

<script>
import ProductList from './components/ProductList.vue'

export default {
  name: 'App',
  components: {
    ProductList
  }
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
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 5rem;
}
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
td, th{
  padding: 0.5rem;
}

.modal-group {
  margin: 1rem;
  display: flex;
  flex-direction: column;
  align-items: start;
}
</style>
