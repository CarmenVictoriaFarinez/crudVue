<template>
  <div id="app">
    <create-product @createProduct="createProduct" />
    <TableList :products="products" @saveProduct="updateProduct" @deleteProduct="deleteProduct" />
  </div>
</template>

<script>
import TableList from './components/TableList';
import CreateProduct from './components/CreateProduct';

export default {
  name: 'App',
  components: {
    TableList,
    CreateProduct
  },
  data() {
    return {
      products: [
        {id: 1, name: 'Angular', description: 'Superheroic JavaScript MVW Framework.', price: 10},
        {id: 2, name: 'Ember', description: 'A framework for creating ambitious web applications.', price: 20},
        {id: 3, name: 'React', description: 'A JavaScript Library for building user interfaces.', price: 30}
      ],
    }
  },
  methods: {
    createProduct(product) {
      this.products.push(product);
    },
    updateProduct(data) {
      this.products = this.products.map(product => product.id === data.id ? {...product, ...data} : product)
    },
    deleteProduct(id) {
      this.products = this.products.filter(product => product.id !== id)
    }
  }
}
</script>


