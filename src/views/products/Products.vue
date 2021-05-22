<template>
  <div>
    <div>
      <v-btn color="primary" elevation="2" href="/products/create">Add</v-btn>
    </div>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">
              #
            </th>
            <th class="text-left">
              Image
            </th>
            <th class="text-left">
              Title
            </th>
            <th class="text-left">
              Description
            </th>
            <th class="text-left">
              Price
            </th>
            <th class="text-left">
              Action
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="product in products.slice((page-1)*perPage,page*perPage)"
            :key="product.id"
          >
            <td>{{ product.id }}</td>
            <td>
              <v-img :src="product.image" height="80" width="120"/>
            </td>
            <td>{{ product.title }}</td>
            <td>{{ product.description }}</td>
            <td>{{ product.price }}</td>
            <td></td>
            <td>
            <v-btn-toggle>
              <v-btn color="primary" elevation="2" :href="`products/${product.id}/edit`">Edit</v-btn>
              <v-btn color="error" elevation="2" @click="del(product.id)">Delete</v-btn>
            </v-btn-toggle>
            </td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
    <div class="text-center">
      <v-pagination
        v-model="page"
        total-visible="perPage"
        :length="lastPage"
      ></v-pagination>
    </div>
  </div>
</template>
<script lang="ts">
import axios from "axios";
export default {
  name: "Products",
  data() {
    return {
      products: [],
      page: 1,
      perPage: 10,
      lastPage: 0
    }
  },
  async mounted(){
      const {data} = await axios.get('products');
      this.products = data;
      this.lastPage = Math.ceil(this.products.length/this.perPage);
  },
  methods:{
    async del(id:number){
      if(confirm("are you sure?")){
        const {status} = await axios.delete(`products/${id}`);
        if(status === 204){
          this.products = this.products.filter((p)=>{
            return p.id !== id;
          })
        }
      }
    },
  }
}
</script>
<style>
  
</style>