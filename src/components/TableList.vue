<template id="table-list">
  <div class="container p-5">
    <!--<h2 class="font-semibold">Add new product</h2>
        <form @submit.prevent="createProduct()" ref="form">
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
        </form>-->
    <h2 class="pt-5 font-semibold">Listado</h2>
    <table class="">
      <thead>
        <tr class="bg-green-200">
          <th>id</th>
          <th>Name</th>
          <th>Description</th>
          <th>Price</th>
          <th class="">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product of products" :key="product.id">
          <template v-if="form_update && (update.id === product.id)">
              <td>{{ update.id }}</td>
              <td>
                  <span>
                    <input v-model="update.name" type="text" class="form-control">
                  </span>
              </td>
              <td>
                <span>
                    <input v-model="update.description" type="text" class="form-control">
                </span>
              </td>
              <td>
                  <span>
                    <input v-model="update.price" type="text" class="form-control">
                  </span>
              </td>
              <td>
                  <span>
                    <button @click="saveProduct" class="bg-green-500">Guardar</button>
                  </span>
              </td>
          </template>
          <template v-else>
              <td>{{ product.id }}</td>
              <td>
                  <span>
                  {{ product.name }}
                  </span>
              </td>
              <td>
                <span>
                    {{ product.description }}
                </span>
              </td>
              <td>
                <span>
                    {{ product.price }}
                </span>
              </td>
              <td>
                <!-- Botón para guardar la información actualizada -->
                  <span>
                    <button type="button" class="bg-yellow-400"  @click="updateProduct(product.id)">Edit</button>
                    <button type="button" class="bg-red-400" @click="deleteProduct(product.id)">Delete</button>
                  </span>
              </td>
          </template>
          
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'table-list',
  props: {
    products: {
      type: Array,
      default: null
    }
  },
 data () {
    return {
      form_update: false,
      update:{},
      product: {
        id: '',
        name: '', 
        description: '', 
        price: ''
      }
    }
  },
  methods: {
    createProduct() {
      this.products.push({...this.product, id: Date.now()});
      //console.log(product)
    },
     updateProduct: function (product_id){
      this.form_update = true;
      this.update = this.products.find(product => product.id === product_id)

      //console.log(this.update);
    },
    
     deleteProduct: function (id) {
      this.$emit('deleteProduct', id)

     },

     saveProduct: function () {
        // Ocultamos nuestro formulario de actualizar
        this.form_update = false;
        // Actualizamos los datos
        
        
        this.$emit('saveProduct', this.update)

     },
 } 
}

</script>

