<script setup lang="ts">
import CensusFormCheckboxes from '@/components/CensusFormCheckboxes.vue'
import CensusFormRadioButton from '@/components/CensusFormRadioButton.vue'
import { computed, ref } from 'vue'

const currentStep = ref(1)
const totalSteps = 5 // Puedes cambiar este número si quieres más o menos pasos

const nextStep = () => {
  if (currentStep.value < totalSteps) {
    currentStep.value++
  }
}

const previousStep = () => {
  if (currentStep.value > 1) {
    currentStep.value--
  }
}

const currentComponent = computed(() => {
  switch (currentStep.value) {
    case 1:
      return CensusFormRadioButton
    case 2:
      return CensusFormCheckboxes
    // Puedes agregar más casos aquí para los pasos restantes
    default:
      return null // O un componente por defecto si lo prefieres
  }
})
</script>

<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-100 p-4">
    <div class="w-full max-w-3xl bg-white rounded-lg shadow-md p-6">
      <ProgressSteps :current-step="currentStep" :total-steps="totalSteps" />
    
      <div class="mt-6 w-full">
        <!-- <p class="text-sm font-semibold mb-4 text-gray-700">Paso {{ currentStep }} de {{ totalSteps }}</p> -->
        
        <component :is="currentComponent" v-if="currentComponent" />
        <p v-else class="text-center text-gray-500">Contenido para el paso {{ currentStep }} no disponible</p>

        <div class="flex justify-center space-x-4 mt-6">
          <button 
            @click="previousStep" 
            class="px-4 py-2 text-sm bg-gray-300 text-gray-700 rounded-md hover:bg-gray-400 transition-colors"
            :disabled="currentStep === 1"
          >
            Regresar
          </button>
          <button 
            @click="nextStep" 
            class="px-4 py-2 text-sm bg-teal-500 text-white rounded-md hover:bg-teal-600 transition-colors"
            :disabled="currentStep === totalSteps"
          >
            Siguiente
          </button>
        </div>
      </div>
    </div>
  </div>
</template>