<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Personas</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <formulario-persona @add-persona="agregarPersona"/>
        <!-- <TablaPersonas :personas="personas"/> -->
        <tabla-personas v-bind:personas="personas" @delete-persona="eliminarPersona" @actualizar-persona="actualizarPersona"/>
      </div>
    </div>
  </div>
</template>

<script>
import TablaPersonas from '@/components/TablaPersonas.vue';
import FormularioPersona from '@/components/FormularioPersona.vue';

export default {
  name: 'App',
  components: {
    TablaPersonas,
    FormularioPersona
  },
  data() {
    return {
      personas: [
        {
          id: 1,
          nombre: 'Joel',
          apellido: 'Miller',
          videojuego: 'The Last of Us'
        },
        {
          id: 2,
          nombre: 'Ellie',
          apellido: 'Williams',
          videojuego: 'The Last of Us'
        },
        {
          id: 3,
          nombre: 'Nathan',
          apellido: 'Drake',
          videojuego: 'Uncharted'
        }
      ]
    }
  }, methods: {
    agregarPersona(persona) {
      let id = 0;
      if (this.personas.length > 0) 
        id = this.personas.length;
      this.personas = [...this.personas, {...persona, id}]
    },
    eliminarPersona(id) {
      this.personas = this.personas.filter(
        persona => persona.id !== id
      )
    },
    actualizarPersona(id, personaActualizada) {
      this.personas = this.personas.map(persona => 
        persona.id === id ? personaActualizada: persona
      )
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
