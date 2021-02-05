<template>
	<h1>{{ msg }}</h1>

  <div class="container">
          <div class="columns is-multiline">
            <div class="column is-one-quarter">
                <div class="select">
                    <select class="is-hovered" id="categories_select" v-model="category">
                      <option v-for="c in categories"
                                v-bind:key="c.categori_id" :id="c.categori_id">{{c.name}}</option>
                    </select>
                  </div>
            </div>

            <div class="column is-one-quarter">
             <input type="text" class="input" placeholder="Search" v-model="name">
            </div>

             <div class="column is-one-quarter">
             <input type="number" class="input" placeholder="Search by price" min=0 v-model="price">
            </div>

          </div>
  </div>

   <div class="container">
          <div class="columns is-multiline">
            <div class="column is-one-quarter"
             v-for="item in filterProducts"
                v-bind:key="item.id">
             <Product  :pd="item"  /> 
            </div>
          </div>
    </div>

</template>
<script>
import Product  from '@/components/Product.vue'

export default {
  name: 'ApiTest',
  components:{ Product},
  data () {
    return { 
     products: [],
     categories: [],
     category: '',
     name: '',
     price: 5000
    }
  },
  props: {
    msg: String
  },
  created () {
    this.load()
  },
  methods: {
    load () {
     fetch('https://my-json-server.typicode.com/TASNETWORK/Prueba-DJunior/products')
      .then(response => response.json())
      .then(data => this.products = data);

      fetch('https://my-json-server.typicode.com/TASNETWORK/Prueba-DJunior/categories')
      .then(response => response.json())
      .then(data => this.categories = data);
    },

     filterProductsByName: function(products) {
        return products.filter(product => !product.name.indexOf(this.name))
     },

    filterProductsByCategory: function(products){
        return products.filter(product => !product.categories.indexOf(this.categori))
    },

    filterProductsByPrice: function(products){
       return products.filter(product => (product.price > 0 && product.price <= this.price) ? product : '')
    }
  },
  computed : {
     filterProducts () {
        return this.filterProductsByPrice(this.filterProductsByName(this.products))
    }

  }

}
</script>
