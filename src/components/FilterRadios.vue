<script setup>
const emit = defineEmits(['filter'])
const filter = (e) => {
  emit('filter', e.target.value)
}
</script>

<template>
  <label class="flex mr-4 items-center flex-nowrap">
    <input type="radio" name="show" value="all" checked @change="filter">
    <span class="whitespace-nowrap ml-1">Show All</span>
  </label>
  <label class="flex mr-4 items-center flex-nowrap">
    <input type="radio" name="show" value="apple" @change="filter">
    <span class="whitespace-nowrap ml-1">Apple</span>
  </label>
  <label class="flex mr-4 items-center flex-nowrap">
    <input type="radio" name="show" value="others" @change="filter">
    <span class="whitespace-nowrap ml-1">Others</span>
  </label>
</template>