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
    background-color: rgb(146, 16, 16);
    color: rgb(0, 0, 0);
  }
</style>
