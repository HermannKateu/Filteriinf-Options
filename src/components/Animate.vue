<template>
  <div>
    <button class="px-6 py-1.5 bg-gray-300 rounded my-2 cursor-pointer" @click="increment"> Click me </button>
    <div :class="['w-full h-[800px] bg-red-200', value === 1 ? 'relative' : '']">
      STEP 1
      <div :class="['w-11/12 h-[700px] bg-blue-200 mx-auto cursor-pointer', value === 2 ? 'relative' : '']">
        STEP 2
        <div :class="['w-10/12 h-[600px] bg-green-200 mx-auto', value === 3 ? 'relative' : '']">
          STEP 3
          {{ value }}
          <LoaderWrapper />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">

import {ref} from "vue";
import LoaderWrapper from "./LoaderWrapper.vue";
const value = ref(3)
const increment = () => --value.value;
</script>