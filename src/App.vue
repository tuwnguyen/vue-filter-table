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
    <DataTable :items="items"/>
  </div>
</template>
