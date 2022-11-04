<template>
  <div class="container-fluid mt-3">
    <div class="jumbotron">
      <h1>Parcial NT2</h1>
      <br>
      <Navbar />
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import Navbar from './componentes/Navbar.vue'

export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>
  .jumbotron {    
    color: rgb(17, 16, 16); 
  }
</style>
