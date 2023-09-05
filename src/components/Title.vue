<script setup>
const props = defineProps({
  title: String
})

const emit = defineEmits(['remove', 'toggle'])
</script>

<template>
  <div class="title">
    {{ title }}
    <div class="ml-auto">
      <i class="icon-chevron-down" @click="emit('toggle')"></i>
      <i class="icon-remove" @click="emit('remove')"></i>
    </div>
  </div>
</template>
