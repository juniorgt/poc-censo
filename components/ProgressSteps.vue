<template>
  <div class="flex items-center justify-center w-full py-4 bg-gray-100 rounded-lg shadow-sm">
    <div class="relative flex items-center justify-between w-full max-w-3xl px-4">
      <!-- Línea de fondo continua (gris) -->
      <div class="absolute top-5 h-2 bg-gray-300 left-[calc(4px+1.25rem)] right-[calc(4px+1.25rem)]"></div>
      
      <!-- Línea de progreso (verde) -->
      <div 
        class="absolute top-5 h-2 bg-teal-500 left-[calc(4px+1.25rem)]" 
        :style="{ width: progressWidth }"
      ></div>
      <template v-for="step in 5" :key="step">
        <div class="flex flex-col items-center z-10">
          <div 
            class="relative flex items-center justify-center w-10 h-10 rounded-full border-2 border-white shadow-md"
            :class="step <= currentStep ? 'text-white bg-teal-500' : 'text-gray-500 bg-gray-300'"
          >
            <UIcon :name="getIconName(step)" class="w-5 h-5" />
          </div>
          <div 
            class="mt-2 text-sm font-semibold text-center"
            :class="step <= currentStep ? 'text-gray-700' : 'text-gray-500'"
          >
            {{ step }}
          </div>
        </div>
      </template>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  currentStep: {
    type: Number,
    required: true
  }
})

const progressWidth = computed(() => {
  const totalSteps = 5
  const stepWidth = 100 / (totalSteps - 1)

  if (props.currentStep === 1) {
    return '0%'
  } 
  if (props.currentStep === totalSteps) {
    return 'calc(100% - 4.25rem)' // Ajustado para evitar que sobresalga
  } 
  const baseWidth = (props.currentStep - 1) * stepWidth
  const remainingSteps = totalSteps - props.currentStep
  const adjustment = (remainingSteps * 0.25) + 2 // 0.25rem por cada paso restante + 2rem base
  return `calc(${baseWidth}% - ${adjustment}rem)`
})

const getIconName = (step) => {
  const icons = [
    'i-heroicons-map-pin',
    'i-heroicons-phone',
    'i-heroicons-home',
    'i-heroicons-users',
    'i-heroicons-check'
  ]
  return icons[step - 1]
}
</script>

<style scoped>
/* Aquí puedes agregar estilos adicionales si es necesario */
</style>
