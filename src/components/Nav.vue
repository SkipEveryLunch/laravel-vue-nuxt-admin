<template>
  <div>
    <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0">
      <router-link  to="/profile" class="navbar-brand col-sm-3 col-md-2 mr-0" href="#">{{`${user.first_name} ${user.last_name}`}}</router-link>
      <a class="nav-link" href="#" @click="logout">Log out</a>
    </nav>
  </div>
</template>
<script  lang="ts">
import axios from 'axios'
export default {
  name:"Nav",
  methods:{
    async logout(){
      await axios.delete('logout');
      this.$router.push("/login");
    }
  },
  computed:{
    user(){
      return this.$store.state.user;
    }
  }
}
</script>