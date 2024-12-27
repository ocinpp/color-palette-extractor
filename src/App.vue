<template>
  <div class="min-h-screen bg-gray-100 py-8 flex flex-col">
    <div class="container mx-auto px-4 flex-grow">
      <h1 class="text-3xl font-bold text-center mb-8">
        Image Colour Palette Extractor
      </h1>
      <ImageUploader />
    </div>
    <Footer />
  </div>
</template>

<script setup>
import ImageUploader from "./components/ImageUploader.vue";
import Footer from "./components/Footer.vue";
</script>
