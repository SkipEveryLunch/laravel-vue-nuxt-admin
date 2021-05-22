<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            #
          </th>
          <th class="text-left">
            Code
          </th>
          <th class="text-left">
            Count
          </th>
          <th class="text-left">
            Revenue
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="link in links"
          :key="link.id"
        >
          <td>{{link.id}}</td>
          <td>{{link.code}}</td>
          <td>{{link.orders.length}}</td>
          <td>{{link.orders.reduce((acc,cur)=>{
            return acc + cur.total;
          },0)}}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>
<script>
import axios from "axios";
export default {
  name:"Links",
  data(){
    return{
      links:[]
    }
  },
  async mounted(){
    const {id} = this.$route.params;
    const {data} = await axios.get(`users/${id}/links`)
    this.links = data;
  }
}
</script>
<style lang="">
  
</style>