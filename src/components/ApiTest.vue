<template>
	<h1>{{ msg }}</h1>

  <div class="container">

     <div class="container">
          <table class="table">
            <thead>
              <td>
                Product
              </td>
              <td>
                Price
              </td>
            </thead>
            <tbody>
              <tr v-for="or in order"
                v-bind:key="or.id"
                @dblclick="delOrder(or)"> 
                  <td>{{or.name}}</td> 
                  <td>{{or.name}}</td>
                  <td>{{or.price}}</td>
              </tr>
            </tbody>
          </table>
     </div>

          <div class="columns is-multiline">
            <div class="column is-one-quarter">
                <div class="select">
                    <select class="is-hovered" id="categories_select" v-model="category">
                      <option v-for="c in categories"
                                v-bind:key="c.categori_id">{{c.name}}</option>
                    </select>
                  </div>
            </div>

            <div class="column is-one-quarter">
             <input type="text" class="input" placeholder="Search" v-model="name">
            </div>

             <div class="column is-one-quarter">
             <input type="number" class="input" placeholder="Search by price" min=0 v-model="price">
             <input type="range" v-model="price" min="0" max="500000" step="10"/> 
            </div>

          </div>
  </div>

 

   <div class="container">
          <div class="columns is-multiline">
            <div class="column is-one-quarter"
             v-for="item in filterProducts"
                v-bind:key="item.id"
                @dblclick="addOrder(item.id, item.name, item.price)">
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
     order: [],
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
    },

    addOrder: function(id,name,price) {
        this.order.push({ id: id, name: name, price: price});
    },
    delOrder: function(event) {

        this.order.splice(this.order.indexOf(event), 1);
    }

  },
  computed : {
     filterProducts () {
        return this.filterProductsByPrice(this.filterProductsByName(this.products))
    }

  }

}
</script>
