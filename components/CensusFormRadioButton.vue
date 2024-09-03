<template>
  <div class="bg-white rounded-lg shadow-sm p-4 mb-4 text-center max-w-2xl mx-auto">
    <div class="mb-2 text-xs text-gray-600">
      <strong>Validación 2 de 10 - SECCIÓN II: CARACTERÍSTICAS Y SERVICIOS DE LA VIVIENDA</strong>
    </div>
    <div class="mb-3 text-left">
      <h2 class="mb-1 text-base font-semibold text-gray-800">
        1. EN LA VIVIENDA, EL MATERIAL DE CONSTRUCCIÓN PREDOMINANTE EN LAS PAREDES EXTERIORES ES:
      </h2>
      <p class="text-xs text-teal-600 italic">
        (Lea las alternativas y seleccione solo un código)
      </p>
    </div>
    <div class="space-y-2">
      <div v-for="option in options" :key="option.id" class="relative">
        <input
          type="radio"
          :id="option.id"
          :name="optionGroupName"
          v-model="selectedOption"
          :value="option.id"
          class="sr-only peer"
        />
        <label
          :for="option.id"
          class="flex items-center p-2 bg-white border border-gray-300 rounded-md cursor-pointer transition-all duration-200 ease-in-out peer-checked:border-teal-500 peer-checked:bg-teal-50 hover:bg-gray-50 text-sm"
        >
          <span class="text-gray-700 font-medium mr-2">{{ option.id }}.</span>
          <span class="text-gray-600">{{ option.label }}</span>
        </label>
        <div class="absolute hidden w-4 h-4 peer-checked:flex justify-center items-center top-1/2 right-2 -mt-2 text-teal-600">
          <svg class="w-3 h-3" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd"></path>
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const optionGroupName = 'material-construccion';
const selectedOption = ref(null);

const options = [
  { id: 1, label: '¿Ladrillo o bloque de concreto?' },
  { id: 2, label: '¿Piedra o sillar con cal o cemento?' },
  { id: 3, label: '¿Adobe?' },
  { id: 4, label: '¿Tapia?' },
  { id: 5, label: '¿Quincha (caña con barro)?' },
  { id: 6, label: '¿Piedra con barro?' },
  { id: 7, label: '¿Madera (pona, tornillo o similares)?' },
  { id: 8, label: '¿Triplay / calamina / estera?' }
];
</script>

<style scoped>
/* Aquí puedes agregar estilos adicionales si es necesario */
</style>
