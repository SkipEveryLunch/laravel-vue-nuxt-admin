<template>
  <div>
    <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0">
      <a class="navbar-brand col-sm-3 col-md-2 mr-0" href="#">{{`${user.first_name} ${user.last_name}`}}</a>
      <a class="nav-link" href="#" @click="logout">Log out</a>
    </nav>
  </div>
</template>
<script  lang="ts">
import axios from 'axios'
export default {
  name:"Nav",
  props:['user'],
  methods:{
    async logout(){
      await axios.delete('logout');
      this.$router.push("login");
    }
  }
}
</script>