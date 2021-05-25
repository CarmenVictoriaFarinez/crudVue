<template id="add-product">
    <div class="p-5">
         <h2 class="p-5 font-semibold">Add new product</h2>
          <form @submit.prevent="createProduct">
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
    </div>
</template>

<script>
export default {
 template: 'add-product',
 props: {
   products: {
       type: Array
   },
  },
  data: function () {
    return {
        product: {
            id: '',
            name: '', 
            description: '', 
            price: ''
            }
        }
  },
  methods: {
    createProduct () {
      this.$emit('createProduct', {...this.product, id: Date.now()})
    }
  }
}

</script>

