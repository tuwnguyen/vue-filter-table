<script setup>
import {computed, ref} from 'vue'

const props = defineProps({
  items: {
    type: Array, 
    required: true,
  }
})
const emit = defineEmits(['filterSelectbox'])
const show = ref(false)
const categories = computed(() => {
  // return props.items.map(item => item.category)
  return [...new Set(props.items.map(item => item.category))]
})

const filter = (e) => {
  emit('filterSelectbox', e.target.value)
}
</script>

<template>
  <div class="relative flex items-center w-full px-4">
    <button @click="show = !show" class="w-full flex items-center justify-center py-2 px-4 text-sm font-medium text-gray-900 border-solid hover:bg-indigo-300 rounded-md border border-indigo-300">
      Filter
    </button>
    <div v-if="show" class="absolute top-12 right-0 z-10 w-48 p-3 bg-white rounded-lg shadow">
      <h6 class="mb-3 text-sm font-medium text-gray-900">Category</h6>
      <ul class="space-y-2 text-sm">
        <li v-for="(category, index) in categories" class="flex items-center space-y-0">
          <input 
            :id="`filter_option_${index}`" 
            type="checkbox" 
            :value="category" 
            @change="filter"
            class="w-5 h-5 text-indigo-400 bg-gray-100 border-gray-300 rounded focus:ring-indigo-500 dark:focus:ring-indigo-500 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600" >
          <label :for="`filter_option_${index}`" class="w-full ms-2 text-sm font-medium text-gray-900 dark:text-gray-900">
            {{ category }}
          </label>
        </li>
      </ul>
    </div>
  </div>
</template>