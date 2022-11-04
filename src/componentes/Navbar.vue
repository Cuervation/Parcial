<template >
  <section class="src-componentes-navbar">
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
      <router-link to="/">
        <a class="navbar-brand" href="#">Inicio</a>
      </router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <!-- navegación binding -->
          <li class="nav-item">
            <router-link to="/ingreso">
              <a class="nav-link" href="#">Ingreso</a>
            </router-link>
          </li>

          <!-- navegación estructura -->
          <li class="nav-item">
            <router-link to="/Respuestas">
              <a class="nav-link" href="#">Respuestas</a>
            </router-link>
          </li>
        </ul>
      </div>
    </nav>
  </section>
</template>

<script >
export default {
  name: "src-componentes-navbar",
  props: [],
  mounted() {},
  data() {
    return {};
  },
  methods: {},
  computed: {},
};
</script>

<style scoped lang="css">

</style>
