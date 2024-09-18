# A simple vue carousel implemented using vueuse

Example Usage:
```ts
<script setup lang="ts">
import Carousel from './Carousel.vue';
import CarouselElement from './CarouselElement.vue';
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
```

[Live playground](https://play.vuejs.org/#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).