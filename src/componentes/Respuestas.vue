<template>
  <section class="src-componentes-resultados">
    <div class="jumbotron">
      <h2>Respuestas</h2>
      <hr />

      <div v-if="preguntas.length" class="table-responsive" >
          <table class="table">
              <tr>                  
                  <th>Número</th>                  
                  <th>Respuesta</th>
              </tr>
              <tr v-for="(pregunta,index) in preguntas" :key="index">                  
                  <td>{{ pregunta.numero }}</td>
                  <td>{{ pregunta.respuestas }}</td>
              </tr>
          </table>
      </div>
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
    return {
      preguntas : [
            { numero: 1, respuestas: ['b','d'] },
            { numero: 2, respuestas: ['c'] },
            { numero: 3, respuestas: ['b','e'] },
    ]
    };
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
