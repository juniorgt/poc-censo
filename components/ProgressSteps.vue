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
      <template v-for="(step, index) in totalSteps" :key="index">
        <div class="flex flex-col items-center z-10">
          <div 
            class="relative flex items-center justify-center w-10 h-10 rounded-full border-2 border-white shadow-md"
            :class="index + 1 <= currentStep ? 'text-white bg-teal-500' : 'text-gray-500 bg-gray-300'"
          >
            <UIcon :name="getIconName(index + 1)" class="w-5 h-5" />
          </div>
          <div 
            class="mt-2 text-sm font-semibold text-center"
            :class="index + 1 <= currentStep ? 'text-gray-700' : 'text-gray-500'"
          >
            {{ stepTitles[index] || `Paso ${index + 1}` }}
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
  },
  totalSteps: {
    type: Number,
    required: true
  },
  stepTitles: {
    type: Array,
    default: () => []
  }
})

const progressWidth = computed(() => {
  const stepWidth = 100 / (props.totalSteps - 1)

  if (props.currentStep === 1) {
    return '0%'
  } 
  if (props.currentStep === props.totalSteps) {
    return 'calc(100% - 4.25rem)' // Ajustado para evitar que sobresalga
  } 
  const baseWidth = (props.currentStep - 1) * stepWidth
  const remainingSteps = props.totalSteps - props.currentStep
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
  return icons[(step - 1) % icons.length]
}
</script>

<style scoped>
/* Aquí puedes agregar estilos adicionales si es necesario */
</style>
