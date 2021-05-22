<template>
  <v-app>
    <div>
      <Nav :user="user"/>
      <div class="container-fluid">
        <div class="row">
          <Menu/>
          <main role="main" class="col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">
            <div class="table-responsive">
              <router-view/>
            </div>
          </main>
        </div>
      </div>
    </div>
  </v-app>
</template>
<script lang="ts">
import axios from 'axios'
import Nav from '@/components/Nav'
import Menu from '@/components/Menu'
import {User} from '@/models/User'
export default {
  name:'Layout',
  components:{Nav,Menu},
  data(){
    return {
      user:new User()
    }
  },
  async mounted(){
    try{
      const {data} = await axios.get('user');
      this.user = data;      
    }catch(e){
      this.$router.push("/login");
    }
  }
}
</script>