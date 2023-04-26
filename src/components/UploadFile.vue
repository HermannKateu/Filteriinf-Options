<template>
    <div class="h-screen w-full absolute image-background z-50  flex justify-center items-center" v-if="isImageZommed">
        <span class="text-white absolute text-4xl right-10 top-8 cursor-pointer" @click="isImageZommed = false">x</span>
        <img :src="zoomedImageUrl" class="w-[60%] h-[80%] shadow mx-auto border object-center" alt="image-zoom"/>
    </div>
    <form class="w-[400px] mx-auto flex flex-col items-center justify-center h-[500px] bg-gray-200 rounded" id="form">
        <div  class="w-[350px] h-[300px] border-2 rounded-lg border-dotted border-black p-1">
            <img :src="imageUrl" alt="image" class="w-full h-full object-center rounded-md cursor-pointer" @click="zoomImage" id="non-zoomed-image"/>
        </div>
        <div class="flex items-center gap-x-7 w-[350px]">
            <div class="my-4 w-[100px] mx-auto relative">
                <button class="text-semibold bg-sky-300 w-full h-11 rounded !cursor-pointer">Upload File</button>
                <input type="file" @change="uploadImage"  accept="image/jpeg, image/png, image/png" class="absolute w-full h-full border left-0 opacity-0"/>
            </div>
            <button class="text-semibold bg-sky-300 w-[100px] mx-auto h-11 rounded" @click.prevent="sendImage" type="submit">Post Image</button>
        </div>
        <div class="my-2 bg-white h-2 w-[85%] rounded-lg flex items-center gap-x-2">
           <span class="h-2 bg-pink-600 rounded-lg transition-all ease-in-out flex" :style="{width: `${imageloadingProgression}%`}"></span>
        </div>
        <span class="flex" v-if="imageloadingProgression !== 100">{{imageloadingProgression+" %"}}</span>
        <span class="flex" v-else>{{"Image Uploaded!!"}}</span>
    </form>
</template>

<script setup lang="ts">
import axios from "axios";
import {ref} from "vue";

const file = ref<File | null>();
const imageUrl = ref<string>("");
const isImageZommed = ref<boolean>(false);
const imageloadingProgression = ref<number>(0);
const uploadImage = ($event) => {
    file.value = $event.target.files[0];
    if (file.value){
        imageloadingProgression.value = 0;
        const fileReader = new FileReader();
        fileReader.readAsDataURL(file.value)
        fileReader.onload = () => {
            imageUrl.value = fileReader.result as string;
        }
    }
}
const sendImage = (): void => {
    if (file.value) {
        const formData = new FormData();
        formData.append('image', file.value);
        const config = {
            onUploadProgress: function(progressEvent) {
                imageloadingProgression.value = Math.round((progressEvent.loaded / progressEvent.total) * 100);
            }
        }
        axios.post('https://httpbin.org/post', formData, config)
            .then(res => {
                console.log(res)
            })
            .catch(err => console.log(err))
    }
};

const zoomedImageUrl = ref<string>("");

const zoomImage = (): void => {
    isImageZommed.value = true;
    zoomedImageUrl.value = document.getElementById("non-zoomed-image").getAttribute("src");
}
</script>

<style scoped>
.image-background {
  background: rgba(21, 41, 81, 0.73);
  backdrop-filter: blur(1px);
  animation: scale-down;
}

@keyframes scale-down {
    0% {
        @apply transform scale-x-100 opacity-100;
    }

    100% {
        @apply transform scale-x-0 opacity-0;
    }
}
</style>