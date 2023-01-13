<template>
  <div id="formualrio-persona">
    <form @submit.prevent="enviarFormulario" class="mb-2">
      <div class="container">
        <div class="row">
          <div class="col-md-4">
            <div class="form-group">
              <label for="nombre">Nombre</label>
              <input
                ref="nombre"
                v-model="persona.nombre"
                type="text"
                class="form-control"
                :class="{ 'is-invalid': procesando && nombreInvalido }"
                @focus="resetEstado"
              />
            </div>
          </div>

          <div class="col-md-4">
            <div class="form-group">
              <label for="apellido">Apellido</label>
              <input
                v-model="persona.apellido"
                type="text"
                class="form-control"
                :class="{ 'is-invalid': procesando && apellidoInvalido }"
                @focus="resetEstado"
              />
            </div>
          </div>

          <div class="col-md-4">
            <div class="form-group">
              <label for="videojuego">Videojuego</label>
              <input
                v-model="persona.videojuego"
                type="text"
                class="form-control"
                :class="{ 'is-invalid': procesando && videojuegoInvalido }"
                @focus="resetEstado"
              />
            </div>
          </div>
        </div>

        <div class="row text-center">
          <div class="con-md-4">
            <div class="form-group">
              <button class="btn btn-primary">Añadir persona</button>
            </div>
          </div>
        </div>

        <div class="container">
          <div class="row">
            <div class="col-md-12">
              <div
                v-if="error && procesando"
                class="alert alert-danger"
                role="alert"
              >
                Debes rellenar todos los campos!
              </div>
              <div v-if="correcto" class="alert alert-success" role="alert">
                La persona ha sido registada correctamente!
              </div>
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "formulario-persona",
  data() {
    return {
      procesando: false,
      correcto: false,
      error: false,
      persona: {
        nombre: "",
        persona: "",
        apellido: "",
      },
    };
  },
  methods: {
    enviarFormulario() {
      this.procesando = true;
      this.resetEstado();

      // Comprobamos que los campos han sido rellenados
      if (
        this.nombreInvalido ||
        this.apellidoInvalido ||
        this.videojuegoInvalido
      ) {
        this.error = true;
        return;
      }

      this.$emit("add-persona", this.persona);
      this.$refs.nombre.focus();

      this.error = false;
      this.correcto = true;
      this.procesando = false;

      // Reestablecer las variables
      this.persona = {
        nombre: "",
        apellido: "",
        videojuego: "",
      };
    },
    resetEstado() {
      this.correcto = false;
      this.error = false;
    },
  },
  computed: {
    nombreInvalido() {
      return this.persona.nombre.length < 1;
    },
    apellidoInvalido() {
      return this.persona.apellido.length < 1;
    },
    videojuegoInvalido() {
      return this.persona.videojuego.length < 1;
    },
  },
};
</script>

<style scoped></style>
