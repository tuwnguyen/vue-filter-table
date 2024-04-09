<script setup>
import DataTable from './components/DataTable.vue';
import {ref, onMounted} from 'vue'
const items = ref([])

onMounted(async () => {
  const response  = await fetch("https://dummyjson.com/products")
  items.value = (await response.json()).products
})

</script>

<template>
  <div class="p-8 bg-gray-100 min-h-screen">
    <h1 class="text-center uppercase text-indigo-500 text-2xl">Filter Data Table</h1>
    <DataTable :items="items"/>
  </div>
</template>
