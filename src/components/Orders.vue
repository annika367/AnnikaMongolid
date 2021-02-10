<template>
  <div>
    <h2 class="mb-3">Tellimused</h2>
    <!-- <p>Count: {{ count }}</p>
    <button @click="addCount()">+</button>
    <button @click="removeCount()">-</button> -->

    <!-- Tellimuste tabel -->
    <b-table striped hover :items="items" :fields="fields">
      <template #cell(price)="data">
        <b class="text-info">{{ data.value }} EUR </b>
      </template>

      <template #cell(actions)="data">
        <b-button variant="success" @click="showProducts(data.item.products)">Vaata tooteid</b-button>
        <!-- <b class="text-info">{{ data.item.products }} EUR </b> -->
      </template>

    </b-table>  
    
    <!-- Toodete tabel -->
    <b-table striped hover :items="productItems" :fields="productFields">
      
      
    </b-table>  

    <!-- <b-table striped hover :items="items" :fields="fields">
      <template #cell(client)="data">
        <b class="text-info">{{ data.value.lastName.toUpperCase() }}</b>, <b>{{ data.value.firstName }}</b>
      </template>
    </b-table> -->
    
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Orders',
  data() {
    return {
      count: 0,
      fields: ['orderID', 'toWhom', 'toCity'],
      // fields: ['client' 'orderDate', 'status', { key: 'price', label: 'Hind!'}, 'action'],
      items: [],
      productsFields: [],
      productItems: []
        
    }
  },
  async created () {
    const orders = await axios({
      url: 'api/orders',
      method: 'GET',
      headers: {}
    })
    console.log('orders', orders)
    this.item = orders.data.allOrders
  },
  methods: {
    showProducts (prodcts) {

    },
    addCount () {
      console.log('Praegune count:', this.count)
      this.count++
    },
    removeCount () {
      console.log('Praegune count:', this.count)
      this.count--
    }  
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>
