<template>
  <div class="flex overflow-hidden w-[350px] border-8 border-black mx-auto my-10">
    <div
        class="flex"
        :style="{
        transform: `translateX(${index}%)`,
        transition: `${transition}`,
      }"
    >
      <div
          class="w-full h-full shrink-0"
          v-for="(color, index) in observer"
          :key="index"
      >
        <div  :class="`h-[300px] bg-${color}-600`">
          {{index}}{{color}}
        </div>
      </div>
    </div>
  </div>
  <div class="flex gap-x-5 justify-center">
    <button class="rounded bg-sky-300 px-10 py-2" @click="previous" v-if="index !== 0">L</button>
    <button class="rounded bg-sky-300 px-10 py-2" @click="next" v-if="index !== -900">R</button>
  </div>
</template>


<script setup lang="ts">
import { computed, ref } from "vue";

const colors = ["red", "blue", "green", "yellow", "orange", "purple", "green", "violet",  "indigo", "pink"];
const observer = computed(() => colors);
const index = ref(0);
const transition = ref<string>("transform 0.8s ease");
const next = () => {
  if (index.value === -900) {
    transition.value = "none";
    return;
  } else {
    transition.value = "transform 0.2s ease";
    index.value -= 100;
  }
};

const previous = () => {
  if (index.value <= -100) {
    transition.value = "transform 0.2s ease";
    index.value += 100;
  } else {
    transition.value = "none";
    return;
  }
};

</script>
