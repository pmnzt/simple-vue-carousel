<script setup lang="ts">
import Carousel from '../Carousel.vue';
import CarouselElement from '../CarouselElement.vue';
const slides = [
  'https://images.unsplash.com/photo-1725714834625-7773f48389db?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxmZWF0dXJlZC1waG90b3MtZmVlZHwzNHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1725109431834-bed0465b6302?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxmZWF0dXJlZC1waG90b3MtZmVlZHw2MHx8fGVufDB8fHx8fA%3D%3D',
  'https://images.unsplash.com/photo-1723877896976-8eb1cc6f07b1?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxmZWF0dXJlZC1waG90b3MtZmVlZHw4MHx8fGVufDB8fHx8fA%3D%3D'
];
</script>

<template>
  <Carousel class="max-w-[20em] relative" :duration="2000" loop>
    <CarouselElement :class="['h-[10em]']" v-for="(slide) in slides">
      <img :src="slide" class="w-full h-full object-cover" />
    </CarouselElement>
    <template #controls="{ jump, currentActiveIndex }">
      <div class="flex justify-center gap-1 py-1 absolute bottom-2 left-1/2 -translate-x-1/2">
        <button @click="jump(index)" class="rounded bg-white w-7 h-2 hover:bg-blue-500" :class="{'!bg-blue-600': index === currentActiveIndex }" v-for="(i, index) in slides"/>
      </div>
    </template>
  </Carousel>
</template>