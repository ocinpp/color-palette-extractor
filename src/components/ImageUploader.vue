<script setup>
import { ref } from "vue";
import ColorThief from "colorthief";
import ColorPalette from "./ColorPalette.vue";
import LoadingSpinner from "./LoadingSpinner.vue";

const imagePreview = ref(null);
const colors = ref([]);
const isProcessing = ref(false);
const colorThief = new ColorThief();

const handleImageUpload = (event) => {
  const file = event.target.files[0];
  if (!file) return;

  isProcessing.value = true;
  colors.value = [];

  const reader = new FileReader();
  reader.onload = (e) => {
    imagePreview.value = e.target.result;

    const img = new Image();
    img.onload = () => {
      const palette = colorThief.getPalette(img, 5);
      colors.value = palette.map(
        ([r, g, b]) =>
          "#" + [r, g, b].map((x) => x.toString(16).padStart(2, "0")).join("")
      );
      isProcessing.value = false;
    };
    img.src = e.target.result;
  };
  reader.readAsDataURL(file);
};
</script>

<template>
  <div class="max-w-4xl mx-auto p-4">
    <div class="mb-8">
      <label
        for="image-upload"
        class="block w-full p-4 text-center border-2 border-dashed border-gray-300 rounded-lg cursor-pointer hover:border-gray-400 transition-colors"
      >
        <span class="text-gray-600">Click to upload an image</span>
        <input
          type="file"
          id="image-upload"
          accept="image/*"
          class="hidden"
          @change="handleImageUpload"
        />
      </label>
    </div>

    <div v-if="imagePreview" class="space-y-4">
      <img
        :src="imagePreview"
        alt="Uploaded image"
        class="w-full h-auto rounded-lg shadow-lg"
      />
      <div v-if="isProcessing" class="py-8">
        <LoadingSpinner />
        <p class="text-center text-gray-600 mt-2">Extracting colors...</p>
      </div>
      <ColorPalette v-else-if="colors.length" :colors="colors" />
    </div>
  </div>
</template>
