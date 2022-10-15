<template>
  <section class="w-[650px] mx-auto py-4">
    <div class="flex space-x-3 my-4 border-b border-blue-400 py-4">
      <input type="text" class="outline-none border border-gray-500 rounded px-2 placeholder:text-gray py-1.5 w-[500px]"
             placeholder="Search your option..."
      v-model="value"
             @input="resetOptions"
      />
      <button class="border px-12 py-1.5 flex bg-blue-600 text-white rounded font-bold" @click.prevent="[counter++ , search]">Search</button>
    </div>
    <div class="flex flex-col space-y-2 h-[460px] overflow-auto">
      <div class="flex item-center space-x-2"  v-for="message in selectedOptions">
         <input type="checkbox" class="w-4 h-4 mt-1.5"/>
            <span class="flex items-center justify-center">{{ message }}</span>
         </div>
    </div>
  </section>
</template>

<script setup>
import { ref, watch } from "vue";

const value = ref("");
const selectedOptions = ref(["hermann", "sontia", "junior","kateu","leopole",
  "ulrich","beki","wilfred","frack","loin",
  "Karteur", "Soclose", "Pladneur", "Avater","Killer","junior","kateu","junior","kateu","junior","kateu"
]);
const options = [...selectedOptions.value];
const counter = ref(0)

const search = () => {
  return selectedOptions.value.filter((option) => option.toLowerCase().replace(/\s+/g, "").includes(value.value.toLowerCase().replace(/\s+/g, "")))
};

const resetOptions = () => {
  if(value.value)return;
  return selectedOptions.value = options
}

watch(() => counter.value, (newValue) => {
  if(counter.value === newValue) {
    selectedOptions.value = search()
  }
  if (value.value.length === 0 ) {
    selectedOptions.value = options
  }
})
</script>

<style>
::-webkit-scrollbar {
  width: 5px;
}

::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px grey;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  background: grey;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
  background: grey;
}
</style>