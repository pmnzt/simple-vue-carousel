<script setup lang="ts">
import Carousel from '../Carousel.vue';
import CarouselElement from '../CarouselElement.vue';
const slides = 3;
</script>

<template>
  <Carousel class="max-w-[20em]" :duration="2000" loop>
    <CarouselElement :class="[['bg-red-600', 'bg-green-600', 'bg-blue-600'][index % slides], 'h-[10em]']" v-for="(slide, index) in slides">
      slide {{ slide }}
    </CarouselElement>
    <template #controls="{ jump, currentActiveIndex }">
      <div class="flex justify-center gap-1 py-1">
        <button @click="jump(index)" class="bg-black w-5 h-3 hover:bg-blue-500" :class="{'!bg-blue-600': index === currentActiveIndex }" v-for="(i, index) in slides"/>
      </div>
    </template>
  </Carousel>
</template>