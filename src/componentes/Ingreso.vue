<template >
  <section class="src-componentes-ingreso">
    <div class="jumbotron">
      <h2>Ingreso de Gastos</h2>
      <hr />      
      <br />
      <vue-form :state="formState" @submit.prevent="guardar()">
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text" 
            id="nombre" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.nombre" 
            name="nombre"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            no-espacios
          >          
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <div slot="maxlength" class="alert alert-danger mt-1">
              Este campo no debe superar los {{ nombreMaxLength }} caracteres.
            </div>            
            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no permite espacios intermedios
            </div>

          </field-messages>
        </validate>

        <br />
        <validate tag="div">
          <label for="descripcion">Descripcion</label>
          <input
            type="text"
            id="descripcion"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.descripcion"
            name="descripcion"
            required                        
          />          
          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
          </field-messages>
        </validate>
        <br>
        <validate tag="div">
          <label for="importe">Importe</label>
          <input 
            type="number" 
            id="importe" 
            class="form-control" 
            autocomplete="off"
            v-model.number="formData.importe" 
            name="importe"
            required
          >
          <!-- mensajes de validación -->
          <field-messages name="importe" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
          </field-messages>
        </validate>
        <button class="btn btn-success my-3" :disabled="formState.$invalid">
          Enviar
        </button>
      </vue-form>    
      <br>
      <hr>
      <hr> 
      <h2>Detalle de Gastos</h2>    
      <hr>
      <div class="col-md-4">
        <label for="presupuesto">Presupuesto</label>
          <input 
            type="number" 
            id="presupuesto" 
            class="form-control" 
            autocomplete="off"            
            v-model.number="presupuesto" 
            placeholder="Ingrese el presupuesto"
            name="presupuesto" 
            @change=  analizarPresupuesto()
            >
        </div>
      <hr>        
      
      <div v-if="gastos.length" class="table-responsive" >
          <table class="table">
              <tr>                  
                  <th>Nombre</th>                  
                  <th>Descripcion</th>
                  <th>Importe</th>                  
                  <th>Fecha</th>                                    
              </tr>
              <tr v-for="(gastos,index) in gastos" :key="index">                  
                  <td>{{ gastos.nombre }}</td>
                  <td>{{ gastos.descripcion }}</td>
                  <td>{{ "$" +  gastos.importe }}</td>
                  <td>{{ gastos.fecha }}</td>                                    
              </tr>
              <tr :style="{'font-weight': 'bold', 'color': analizarPresupuesto().color }" > 
                  <td></td>                                    
                  <td>TOTAL</td>                  
                  <td>{{ "$" + this.sumaImporte }}</td>                                    
              </tr>              
          </table>
      </div>
      <h4 v-else class="alert alert-danger text-center">
        No se encuentran gastos
      </h4>    
  </div>
  </section>
</template>

<script >
export default {
  name: "src-componentes-ingreso",
  props: [],
  mounted() {},
  data() {
    return {
      gastos:[],
      sumaImporte : 0,
      presupuesto:'',
      formState: {},
      formData: this.getInitialData(),
      nombreMinLength: 3,
      nombreMaxLength: 15,
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: null,
        descripcion: null,
        importe: null,
        fecha: null,        
      }
    },      
    guardar() {
      let gasto = { ...this.formData }
      gasto.fecha = new Date().toLocaleString()
      this.sumaImporte += gasto.importe      
      this.gastos.push(gasto);
      console.log(this.presupuesto);
      this.formData = this.getInitialData();
      this.formState._reset();
      },
    analizarPresupuesto() {        
      let color = 'orange'      
      if (this.presupuesto > this.sumaImporte){
        color = 'red'
      }
      else if(this.sumaImporte < 1000) color = 'green'
      else if(this.sumaImporte <= 5000) color = 'magenta'
      return {          
        color
      }


      

    }
  },
  computed: {},
};
</script>

<style scoped lang="css">

  .jumbotron {
    background-color: rgb(194, 198, 226);
    color: rgb(45, 13, 125);
  }

  hr {
    background-color: #bbb;
  }


</style>
