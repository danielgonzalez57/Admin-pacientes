<script setup>
import {ref, reactive} from 'vue'
import {uid} from 'uid'
import Header from './components/Header.vue'
import Formulario from './components/formulario.vue'
import Paciente from './components/Pacientes.vue'

const pacientes = ref([]);

const paciente = reactive({
        id: null,
        nombre: '',
        propietario: '', 
        email: '', 
        alta: '', 
        sintomas: ''
    });

const guardarPaciente = () => {
    pacientes.value.push({  
      ...paciente,
      id: uid()
    });

    // Reiniciar el formulario
    paciente.nombre = ''
    paciente.propietario = ''
    paciente.email = ''
    paciente.alta = ''
    paciente.sintomas = ''
}


</script>

<template>
      <div class="container mx-auto mt-20">
        <Header />

        <div class="mt-12 md:flex">
          <Formulario 
            v-model:nombre="paciente.nombre"
            v-model:propietario="paciente.propietario"
            v-model:email="paciente.email"
            v-model:alta="paciente.alta"
            v-model:sintomas="paciente.sintomas"
            @guardar-paciente="guardarPaciente"
          />


          <div class="md:w-1/2 md:h-screen overflow-y-scroll">
            <h3 class="font-black text-3xl text-center">Administra tu parientes</h3>

            <div v-if="pacientes.length > 0">
            <p class="text-lg mt-5 text-center mb-10">
              Informacion de
            <span class="text-indigo-600 font-bold">pacientes</span>
            </p>
              <Paciente
                v-for="paciente in pacientes"
                :paciente="paciente"
              />
            </div>
            <p v-else class="mt-10 text-2xl text-center">No hay pacientes</p>
          </div>
        </div>
      </div>
</template>
