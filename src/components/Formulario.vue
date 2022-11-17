<template>
  <section class="src-componentes-formulario">
    <div class="jumbotron">
      <h2>Formulario</h2>
      <hr />
      <hr />
      <br />

      <vue-form :state="formState" @submit.prevent="enviar()">
        <!-- ---------------------------------- -->
        <!--            CAMPO NOMBRE            -->
        <!-- ---------------------------------- -->
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
          />
          <!-- mensajes de validación -->
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <div slot="maxLength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMaxLength }} caracteres.
            </div>
          </field-messages>
        </validate>

        <br />

        <!-- ---------------------------------- -->
        <!--             CAMPO EDAD             -->
        <!-- ---------------------------------- -->
        <validate tag="div">
          <label for="edad">Edad</label>
          <input
            type="number"
            id="edad"
            class="form-control"
            autocomplete="off"
            v-model.number="formData.edad"
            name="edad"
            required
            :min="edadMin"
            :max="edadMax"
          />
          <!-- mensajes de validación -->
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="min" class="alert alert-danger mt-1">
              La edad mínima debe ser {{ edadMin }} años.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La edad máxima debe ser {{ edadMax }} años.
            </div>
          </field-messages>
        </validate>

        <br />

        <!-- ---------------------------------- -->
        <!--            CAMPO EMAIL             -->
        <!-- ---------------------------------- -->
        <validate tag="div">
          <label for="email">Email</label>
          <input
            type="email"
            id="email"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.email"
            name="email"
            required
          />
          <!-- mensajes de validación -->
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="email" class="alert alert-danger mt-1">
              Email no válido
            </div>
          </field-messages>
        </validate>
        <br />

        <button class="btn btn-success my-3" :disabled="formState.$invalid">
          Enviar
        </button>
      </vue-form>

    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      formState: {},
      formData: this.getInitialData(),
      nombreMinLength: 3,
      nombreMaxLength: 15,
      edadMin: 18,
      edadMax: 120,
      usuarios: [],
      ruta: "https://635723ad9243cf412f93b0b0.mockapi.io/usuarioss"
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: null,
        edad: null,
        email: null,
      };
    },
    enviar() {
      this.metodoPost({...this.formData})
      this.formData = this.getInitialData();
      this.formState._reset();
    },
    async metodoPost(usuario){
      try {
          await this.axios.post(this.ruta,usuario)
        }
        catch(error) { console.error(error) } 
        
    }
  },
  computed: {},
};
</script>

<style scoped lang="css">
.jumbotron {
  background-color: purple;
  color: white;
}

hr {
  background-color: #bbb;
}

pre {
  color: white;
}
</style>
