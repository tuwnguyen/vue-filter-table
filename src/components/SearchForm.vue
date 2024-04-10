<script setup>
const emit = defineEmits('search')
const search = (e) => {
  emit('search', e.target.value)
}
</script>

<template>
  <form class="py-3 px-4 flex items-center">
    <label class="sr-only">Search</label>
    <div class="relative w-full">
      <input
        type="text"
        placeholder="Search something"
        class="focus:ring-2 focus:ring-inset p-2 bg-gray-50 border border-gray-500 text-justify text-gray-900 text-sm rounded-md"
        @input="search"  
      >
    </div>
  </form>
</template>