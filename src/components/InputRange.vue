<template>
  <div class="flex flex-col items-center justify-center h-[100vh] gap-y-4">
    <div class="flex relative w-[410px] space-x-0 justify-between items-center rounded">
      <input type="range" id="1" :value="inputValue1" min="0" max="500" class="w-52 slider" @input="affectValue"/>
      <span class="border-y flex h-1.5 w-6 border-gray bg-[#203E79]"></span>
      <input type="range" id="2" class="w-52 slider" :value="inputValue2" min="600" max="1000" @input="affectValue2"/>
    </div>
    <div>
      {{inputValue1+ "-" +inputValue2}}
    </div>
  </div>
</template>

<script setup lang="ts">
import {ref} from "vue";
const inputValue1 = ref("0")
const inputValue2 = ref("1000")

const affectValue = ($event: {
  target: { value: string };
}): void => {
  inputValue1.value = $event.target.value;
}

const affectValue2 = ($event: {
  target: { value: string };
}): void => {
  inputValue2.value = $event.target.value;
}
</script>

<style scoped>
.slider {
  -webkit-appearance: none;
  height: 4px;
  background: #203E79;
  outline: none;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  border-radius: 100%;
  height: 20px;
  background: #203E79;
  cursor: pointer;
}

.slider::-moz-range-thumb {
  width: 25px;
  height: 25px;
  background: #04AA6D;
  cursor: pointer;
}
</style>