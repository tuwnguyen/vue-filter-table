<script setup>
import FilterDropdown from './FilterDropdown.vue';
import FilterRadios from './FilterRadios.vue';
import SearchForm from './SearchForm.vue';
import {computed, ref} from 'vue'
const searchFilter = ref('')
const radioFilter = ref('')
const selectedFilter = ref([])
const props = defineProps({
  items: {
    type: Array,
    required: true,
  }
})

const filteredItems = computed(() => {
  let items = props.items
  
  switch (radioFilter.value) {
    case 'apple':
      items = items.filter(item => item.brand === 'Apple')
      break
    case 'others':
      items = items.filter(item => item.brand !== 'Apple')
      break
    default:
      break
  }

  if (selectedFilter.value.length > 0) {
    items = items.filter(item => selectedFilter.value.includes(item.category))
  }

  if (searchFilter.value !== '')
    return items.filter(
      item =>
      item.title.toLowerCase().includes(searchFilter.value) || 
      item.description.toLowerCase().includes(searchFilter.value))
  return items
})

const handleSearch = (search) => {
  searchFilter.value = search
}

const handleRadioFilter = (filter) => {
  radioFilter.value = filter
}

const handleSelectFilter = (filter) => {
  if (selectedFilter.value.includes(filter)) {
    return selectedFilter.value = selectedFilter.value.filter(item => item !== filter)
  }
    return selectedFilter.value.push(filter)
}
</script>

<template>
  <div class="bg-white relative border rounded-lg">
    <div class="flex items-center justify-between">
      <!-- Search bar -->
      <SearchForm @search="handleSearch"/>

      <div class="flex items-center justify-end text-sm font-semibold">
        <!-- Radio buttons -->
        <FilterRadios @filter="handleRadioFilter"/>

        
        <!-- List of filters -->
        <FilterDropdown :items="items" @filterSelectbox="handleSelectFilter"/>
      </div>
    </div>
    <table class="w-full text-sm text-left text-gray-500">
      <thead class="text-xs text-gray-700 uppercase bg-gray-50">
        <tr>
          <th class="px-4 py-3">ID</th>
          <th class="px-4 py-3">Title</th>
          <th class="px-4 py-3">Description</th>
          <th class="px-4 py-3">Price</th>
          <th class="px-4 py-3">Brand</th>
          <th class="px-4 py-3">
            <span class="sr-only">Actions</span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in filteredItems" :key="item.id" class="border-b">
          <td class="px-4 py-3 font-medium text-gray-900">{{ item.id }}</td>
          <td class="px-4 py-3 font-medium text-gray-900">{{ item.title }}</td>
          <td class="px-4 py-3">{{ item.description }}</td>
          <td class="px-4 py-3">{{ item.price }}</td>
          <td class="px-4 py-3">{{ item.brand }}</td>
          <td class="px-4 py-3 flex items-center justify-end">
            <a href="#" class="text-indigo-500 hover:underline">Details</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
