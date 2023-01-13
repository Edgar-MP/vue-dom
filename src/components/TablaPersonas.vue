<template>
    <div v-if="!personas.length" class="alert alert-info" role="alert">
        No se han agregado personas
    </div>
    <div v-if="personas.length" id="tabla-personas">
        <table class="table">
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Apellido</th>
                    <th>Videojuego</th>
                    <th>Acciones</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="persona in personas" :key="persona.id">
                    <!-- Nombre -->
                    <td v-if="editando === persona.id">
                        <input type="text" class="form-control" v-model="persona.nombre">
                    </td>
                    <td v-else>
                        {{ persona.nombre }}
                    </td>

                    <!-- Apellido -->
                    <td v-if="editando === persona.id">
                        <input type="text" class="form-control" v-model="persona.apellido">
                    </td>
                    <td v-else>
                        {{ persona.apellido }}
                    </td>

                    <!-- Videojuego -->
                    <td v-if="editando === persona.id">
                        <input type="text" class="form-control" v-model="persona.videojuego">
                    </td>
                    <td v-else>
                        {{ persona.videojuego }}
                    </td>

                    <td v-if="editando === persona.id">
                        <button class="btn btn-success"
                            @click="guardarPersona(persona)">💾Guardar</button>
                        <button class="btn btn-secondary mx-2"
                            @click="cancelarEdicion(persona)">❌Cancelar</button>
                    </td>
                    <td v-else>
                        <button class="btn btn-danger"
                            @click="$emit('delete-persona', persona.id)">🗑️Eliminar</button>
                        <button class="btn btn-info mx-2"
                            @click="editarPersona(persona)">✏️Editar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'tabla-personas',
    props: {
        personas: Array,
    },
    data() {
        return {
            editando: null,
        }
    },
    methods: {
        editarPersona(persona) {
            this.personaEditada = Object.assign({}, persona);
            this.editando = persona.id;
        },
        guardarPersona(persona) {
            if (!persona.nombre.length || !persona.apellido.length || !persona.videojuego.length) {
                return;
            }
            this.$emit('actualizar-persona', persona.id, persona);
            this.editando = null;
        },
        cancelarEdicion(persona) {
            Object.assign(persona, this.personaEditada);
            this.editando = null;
        }
    }
}

</script>
<style scoped></style>