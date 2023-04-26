<template>
  <div class="w-[300px] h-[300px] bg-black text-white font-bold text-center text-5xl transition ease-in-out duration-700 lazy-loader">
    {{ label }}
  </div>
</template>

<script setup lang="ts">
defineProps({
  label: {
    type: Number,
  }
})
</script>

<style scoped>
.show {
  @apply inline-flex;
}
.not-show {
  @apply hidden;
}
</style>