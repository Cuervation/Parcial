<template>
  <section class="src-componentes-resultados">
    <div class="jumbotron">
      <h2>Respuestas</h2>
      <hr />

      <table class="table table-p">
        <tr>
          <th>Pregunta</th>
          <th>Respuesta</th>
        </tr>
        <tr>
          <td>1</td>
          <td>A</td>
        </tr>
        <tr>
          <td>2</td>
          <td>C</td>
        </tr>
        <tr>
          <td>3</td>
          <td>B</td>
        </tr>
      </table>
      <hr />
    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-resultados",
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
.src-componentes-resultados {
}
.jumbotron {
  background-color: rgb(198, 240, 238);
  color: rgb(45, 13, 125);
}

hr {
  background-color: #bbb;
}

pre {
  color: white;
}
.table-p {
  background-color: rgb(225, 201, 201);
  color: rgb(31, 12, 97);
}
</style>
