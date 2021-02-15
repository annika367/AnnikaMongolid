<template>
  <div>
    <h2 class="mb-3">Tooted</h2>
       
    <b-table striped hover :items="items" :fields="fields">

    

      <template #cell(actions)="data">
        <b-button v-b-modal.modal-1 variant="success" @click="showProducts(data.item.products, data.item)">Vaata tooteid</b-button>
      </template>

    </b-table>


  <b-modal id="modal-1" :title="productTableTitle" size='xl'>
    <b-table striped hover :items="productItems" :fields="productFields">
      <template #cell(price)="data">
        <b class="text-info">{{ data.value }} EUR</b>
      </template>
    </b-table>
  </b-modal>


  </div>
</template>
<script>
import axios from 'axios'


export default {
  name: 'Products',
  data() {
    return {
      
      count: 0,
      
      fields: ['productCode', 'productName', 'productCat', 'productDescription', { key: 'price', label: 'Hind' }, 'actions'],
      items: [],
      productItems: [],
      productTableTitle: 'Pealkiri'
    }
  },
  async created () {
    const products = await axios({
      url: 'api/products',
      method: 'GET',
      headers: {}
    })
  
    this.items = products.data.allProducts

  },
  methods: {
    showProducts (products, item) {
      console.log('products', products)
      this.productItems = products
      console.log(item)
      this.productTableTitle = item.productId
    }
  }
}
</script>