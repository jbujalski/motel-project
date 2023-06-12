<template>
  <div class="sm:h-screen h-[calc(100vh_-_68px)] pb-4 px-4 sm:p-10">
    <div class="relative w-full h-full overflow-hidden">
      <div class="relative w-full h-full max-w-full overflow-hidden">
        <transition name="slide-fade" mode="out-in">
          <div :key="activeIndex" class="absolute top-0 left-0 w-full h-full flex items-center justify-center">
            <img :src="getImageUrl(slides[activeIndex].image)" :alt="slides[activeIndex].title"
              class="w-full h-full object-cover" />
          </div>
        </transition>
      </div>
      <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 flex justify-center mt-4">
        <button v-for="(slide, index) in slides" :key="index" :class="{ active: activeIndex === index }"
          @click="goToSlide(index)" class="pagination-dot"></button>
      </div>
      <button class="absolute top-1/2 transform -translate-y-1/2 px-2 py-1 cursor-pointer left-4 rotate-180 w-14 h-14"
        @click="prevSlide()">
        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 26 50.9"
          class="w-full h-full fill-none stroke-yellow-700 stroke-2">
          <polyline points="0.4,50.6 25.3,25.5 0.4,0.4 "></polyline>
        </svg>
      </button>
      <button class="absolute top-1/2 transform -translate-y-1/2 px-2 py-1 cursor-pointer right-4 w-14 h-14"
        @click="nextSlide()">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 26 50.9"
          class="w-full h-full fill-none stroke-yellow-700 stroke-2">
          <polyline points="0.4,50.6 25.3,25.5 0.4,0.4 "></polyline>
        </svg>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
const getImageUrl = (name) => {
  return new URL(`../assets/${name}`, import.meta.url).href;
};

const slides = ref([
  {
    image: "slide-bg1.jpeg",
  },
  {
    image: "slide-bg2.jpg",
  },
  {
    image: "slide-bg3.jpeg",
  },
  {
    image: "slide-bg4.jpeg",
  },
]);

const activeIndex = ref(0);
const interval = 10000;

function goToSlide(index) {
  activeIndex.value = index;
}

function prevSlide() {
  activeIndex.value = (activeIndex.value - 1 + slides.value.length) % slides.value.length;
}

function nextSlide() {
  activeIndex.value = (activeIndex.value + 1) % slides.value.length;
}

// Watch for changes in activeIndex and update it automatically after a certain interval
watch(activeIndex, () => {
  setTimeout(() => {
    nextSlide();
  }, interval);
});
</script>

<style scoped>
.slide-fade-enter-active,
.slide-fade-leave-active {
  @apply transition-opacity duration-500;
}

.slide-fade-enter,
.slide-fade-leave-to {
  @apply opacity-0;
}

.pagination-dot {
  @apply w-3 h-3 rounded-full bg-white mx-2 cursor-pointer;
}

.pagination-dot.active {
  @apply bg-yellow-700;
}
</style>
