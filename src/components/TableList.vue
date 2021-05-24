<template id="table-list">
  <div class="container p-5">
    <h2 class="font-semibold">Add new product</h2>
        <form @submit.prevent="createProduct()">
          <div>
              <label for="add-name">Name</label>
              <input class="form-control" id="add-name" v-model="product.name" required/>
          </div>
          <div>
              <label for="add-description">Description</label>
              <input class="form-control" id="add-description" v-model="product.description"/>
          </div>
          <div>
              <label for="add-price">Price <span class=""></span></label>
              <input type="number" class="form-control" id="add-price" v-model="product.price"/>
          </div>
          <button type="submit" class="bg-green-500">Create</button>
        </form>
    <h2 class="pt-5 font-semibold">Listado</h2>
    <table class="">
      <thead>
        <tr class="bg-green-200">
          <th>Name</th>
          <th>Description</th>
          <th>Price</th>
          <th class="">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
           <td>{{ product.id }}</td>
                
           <td>
              <span v-if="formUpdate && idUpdate == product.id">
                 <input v-model="nameUpdate" type="text" class="form-control">
              </span>
              <span v-else>
                    {{ product.name }}
              </span>
           </td>

           <td>
              <span v-if="formUpdate && idUpdate == product.id">
                 <input v-model="descriptionUpdate" type="text" class="form-control">
              </span>
              <span v-else>
                    {{ product.description }}
              </span>
           </td>

          <td>
              <span v-if="formUpdate && idUpdate == product.id">
                 <input v-model="priceUpdate" type="text" class="form-control">
              </span>
              <span v-else>
                    {{ product.price }}
              </span>
           </td>
          <td>
             <!-- Botón para guardar la información actualizada -->
              <span v-if="formUpdate && idUpdate == product.id">
                  <button @click="saveProduct(product.id)" class="bg-green-500">Guardar</button>
              </span>
              <span v-else>

                <button type="button" class="bg-yellow-400"  @click="updateProduct(product.id)">Edit</button>
                <button type="button" class="bg-red-400" @click="deleteProduct(product.id)">Delete</button>

              </span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  template: 'table-list',
  props: [],
 data () {
    return {
      formUpdate: false,
      nameUpdate: '',
      descriptionUpdate:'',
      priceUpdate: '',
      products: [
      {id: 1, name: 'Angular', description: 'Superheroic JavaScript MVW Framework.', price: 10},
      {id: 2, name: 'Ember', description: 'A framework for creating ambitious web applications.', price: 20},
      {id: 3, name: 'React', description: 'A JavaScript Library for building user interfaces.', price: 30}
    ],
      product: {
        name: '', 
        description: '', 
        price: ''
      }
    }
  },
  methods: {
    createProduct () {
    let product = this.product;
      this.products.push({
        id: Date.now(),
        name: product.name,
        description: product.description,
        price: product.price
      }); 
      
    },
     updateProduct: function (product_id){
      this.idUpdate = product_id;
      this.nameUpdate = this.products[product_id].name;
      this.descriptionUpdate = this.products[product_id].description;
      this.priceUpdate = this.products[product_id].price;

      this.formUpdate = true;
      console.log(this.formUpdate)
    },
    
     deleteProduct: function (product_id) {
        // Borramos de la lista
      this.products.splice(product_id, 1);
      console.log(product_id)
     },

     saveProduct: function (product_id) {
        // Ocultamos nuestro formulario de actualizar
        this.formUpdate = false;
        // Actualizamos los datos
        this.products[product_id].name = this.nameUpdate;
        this.products[product_id].description = this.descriptionUpdate;
        this.products[product_id].price = this.priceUpdate;
     },
 } 
}

</script>

