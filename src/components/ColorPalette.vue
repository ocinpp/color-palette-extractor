<script setup>
const props = defineProps({
  colors: {
    type: Array,
    required: true,
  },
});

const copyColors = () => {
  const colorsArray = JSON.stringify(props.colors);
  navigator.clipboard.writeText(colorsArray);
};
</script>

<template>
  <div class="space-y-4">
    <div class="flex flex-col md:flex-row rounded-lg overflow-hidden shadow-lg">
      <div
        v-for="(color, index) in colors"
        :key="index"
        :style="{ backgroundColor: color }"
        class="h-16 md:h-24 md:flex-1"
      >
        <div
          class="h-full flex items-center md:items-end justify-center p-2 bg-black bg-opacity-0 hover:bg-opacity-10 transition-all"
        >
          <span class="text-sm font-mono text-white shadow-sm">{{
            color.toUpperCase()
          }}</span>
        </div>
      </div>
    </div>
    <button
      @click="copyColors"
      class="w-full py-2 px-4 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors"
    >
      Copy Colours Array
    </button>
  </div>
</template>
