<template >
  <section class="src-componentes-formulario">
    <div class="jumbotron">
      <h2>Ingreso de Gastos</h2>
      <hr />
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
            no-espacios
          />
          <!-- mensajes de validación -->
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no permite espacios intermedios
            </div>
          </field-messages>
        </validate>
        <br />
        <validate tag="div">
          <label for="dni">DNI</label>
          <input
            type="text"
            id="dni"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.dni"
            name="nombre"
            required                        
          />
          <!-- mensajes de validación -->
          <field-messages name="dni" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
          </field-messages>
        </validate>
        <br>
        <validate tag="div">
          <label for="pagar">Monto a pagar</label>
          <input 
            type="number" 
            id="pagar" 
            class="form-control" 
            autocomplete="off"
            v-model.number="formData.pagar" 
            name="pagar"
            required
          >
          <!-- mensajes de validación -->
          <field-messages name="pagar" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
          </field-messages>
        </validate>
        <br>
        <validate tag="div">
          <label for="pago">Pago realizado</label>
          <input 
            type="number" 
            id="pago" 
            class="form-control" 
            autocomplete="off"
            v-model.number="formData.pago" 
            name="pago"
            required
          >
          <!-- mensajes de validación -->
          <field-messages name="pago" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
          </field-messages>
        </validate>

        <br>        
        <button class="btn btn-info my-3" :disabled="formState.$invalid">
          Guardar
        </button>
      </vue-form>
    </div>

      <hr>
      
      <div v-if="pagos.length" class="table-responsive" >
          <table class="table table-blue">
              <tr>                  
                  <th>Nombre</th>                  
                  <th>DNI</th>
                  <th>Monto a pagar</th>                  
                  <th>Pago efectuado</th>                  
                  <th>Fecha</th>                  
                  <th>Saldo</th>                  
              </tr>
              <tr v-for="(pago,index) in pagos" :key="index" :style="{ 'color': calcularSaldo(pago).color }">                  
                  <td>{{ pago.nombre }}</td>
                  <td>{{ pago.dni }}</td>
                  <td>{{ pago.pagar }}</td>
                  <td>{{ pago.pago }}</td>
                  <td>{{ pago.fecha }}</td>
                  <td>{{ calcularSaldo(pago).deuda }}</td>
              </tr>
          </table>
      </div>
      <h4 v-else class="alert alert-danger text-center">
        No se encuentran datos
      </h4>    

  </section>
</template>

<script >
export default {
  name: "src-componentes-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      pagos:[],
      formState: {},
      formData: this.getInitialData(),
      nombreMinLength: 3,
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: null,
        dni: null,
        total: null,
        pago: null,
      }
    },      
    guardar() {
      let pago = { ...this.formData }
      pago.fecha = new Date().toLocaleString()
      this.pagos.push(pago);
      this.formData = this.getInitialData();
      this.formState._reset();
      },
      calcularSaldo(pago){
        let deuda = pago.pago - pago.pagar
        let color = 'green'
        if (deuda < 0 ){
          color = 'red'
        }
        else if (deuda > 0 ){
          color =  'blue'
        }
        return { deuda, color }

      }         
  },
  computed: {},
};
</script>

<style scoped lang="css">
.src-componentes-formulario {
}
.jumbotron {
  background-color: rgb(242, 187, 200);
  color: rgb(45, 13, 125);
}

hr {
  background-color: #bbb;
}

pre {
  color: white;
}
.table-blue {
  background-color: rgb(193, 195, 214);
  color: rgb(31, 12, 97);
}
</style>
