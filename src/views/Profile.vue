<template>
  <div>
    <h3 class="mt-4">Account Information</h3>
    <form @submit.prevent="informSubmit">
    <div class="mb-3">
      <v-text-field label="First Name" v-model="user.first_name"/>
    </div>
    <div class="mb-3">
      <v-text-field label="Last Name" v-model="user.last_name"/>
    </div>
    <div class="mb-3">
      <v-text-field label="Email" v-model="user.email"/>
    </div>
    <v-btn color="primary" type="submit" >Submit</v-btn>
  </form>

    <h3 class="mt-4">Change Password</h3>
    <form @submit.prevent="passwordSubmit">
    <div class="mb-3">
      <v-text-field label="Password" v-model="password"/>
    </div>
    <div class="mb-3">
      <v-text-field label="Password Confirmation" v-model="password_confirm"/>
    </div>
    <v-btn color="primary" type="submit" >Submit</v-btn>
  </form>
  </div>
</template>
<script lang="ts">
import User from "@/models/User";
import axios from "axios";
export default {
  name:"Profile",
  data(){
    return {
      password:"",
      password_confirm:""
    }
  },
  computed:{
    user(){
      return this.$store.state.user;
    }
  },
  methods:{
    async informSubmit(){
      const {data,status} = await axios.put("updateInfo",{
        first_name:this.user.first_name,
        last_name:this.user.last_name,
        email:this.user.email,
      })
      if(status===202){
        this.$store.dispatch("setUser",data)
      }
    },
    async passwordSubmit(){
      const {status} = await axios.put("updatePassword",{
        password:this.password,
        password_confirm:this.password_confirm
      })
      if(status===200){
        this.$router.push("/");
      }
    },
  }
}
</script>
<style lang="">
  
</style>