<template>
  <form @submit.prevent="submit">
    <div class="mb-3">
      <v-text-field label="Title" v-model="title"/>
    </div>
    <div class="mb-3">
      <v-textarea label="Description" v-model="description"/>
    </div>
    <div class="mb-3">
      <v-text-field label="Image"
      v-model="image"/>
    </div>
    <div class="mb-3">
      <v-text-field label="Price" type="number" min="0"
      v-model="price"/>
    </div>
    <v-btn color="primary" type="submit" >Submit</v-btn>
  </form>
</template>
<script lang="ts">
import axios from "axios";
export default {
  name:"ProductForm",
  data(){
    return{
      title:"",
      description:"",
      image:"",
      price:""
    }
  },
  async mounted(){
    const id = this.$route.params.id;
    if(id){
      const {data} = await axios.get(`products/${id}`);
      this.title = data.title;
      this.description = data.description;
      this.image = data.image;
      this.price = data.price;
    }
  },
  methods:{
    async submit(){
      const formData = {
        title:this.title,
        description:this.description,
        image:this.image,
        price:this.price
      };
    const id = this.$route.params.id;
    if(id){
      const {status} = await axios.put(`products/${id}`,formData);
      console.log(status);
      if(status===202){
        this.$router.push("/products");
      }
    }else{
        const {status} = await axios.post("products",formData);
      if(status===201){
        this.$router.push("/products");
      }
    }
    }
  }
}
</script>
<style>
  
</style>