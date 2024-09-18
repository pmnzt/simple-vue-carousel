<script setup lang="ts">
import { ref } from 'vue';
import { useScroll, useInterval, useElementBounding } from "@vueuse/core"
import { watch } from 'vue';
type Behavior = 'smooth' | 'instant' | 'auto'
const DEFAULT_DURATION = 5 * (1000)
const DEFAULT_BEHAVIOR: Behavior = 'smooth'

interface CarouselProps {
  duration?: number
  loop?: boolean
  behavior?: Behavior
}

const props = defineProps<CarouselProps>();
const behavior = props.behavior ?? DEFAULT_BEHAVIOR
const duration = props.duration ?? DEFAULT_DURATION

const container = ref<HTMLElement>()
const { width: containerWidth }
  = useElementBounding(container)

function next() {
  if (container.value) {
    container.value.scrollBy({
      left: containerWidth.value,
      behavior,
    });
  }
}

const { x } = useScroll(container)

function isEnd() {
  if (!container.value) return true
  const total = container.value?.scrollWidth - container.value?.clientWidth;
  const isEnd = x.value === total
  return isEnd
}

const { pause, resume } = useInterval(duration, { controls: true, callback: autoSlide })
watch(() => props.loop, (value: boolean) => {
  if (value) {
    resume()
  } else {
    pause()
  }
})

function autoSlide() {
  next()
  if (isEnd() && props.loop) {
    const total = container.value?.scrollWidth - container.value?.clientWidth;

    container.value.scrollBy({
      left: -total,
      behavior
    });
  }
}

function jump(index: number) {
  if (container.value) {
    const total = container.value?.offsetWidth;
    const jumpBy = index * total

    container.value.scrollTo({
      left: jumpBy,
      behavior
    });
  }
}

const currentActiveIndex = ref(0)
watch((x), (value: number) => {
  const scrollX = value;
  const clientWidth = container.value?.clientWidth
  const scrollWidth = container.value?.scrollWidth

  if (clientWidth && scrollWidth) {
    const currentIndex = Math.floor(scrollX / clientWidth);
    currentActiveIndex.value = currentIndex;
  }
})
</script>

<template>
  <div>
    <div ref="container" class="carousel-container hide-scrollbar">
      <slot />
    </div>
    <div @pointerover="pause()" @pointerleave="resume()">
      <slot name="controls" :jump="jump" :currentActiveIndex="currentActiveIndex" />
    </div>
  </div>
</template>

<style scoped>
.carousel-container {
  white-space: nowrap;
  overflow-x: auto;
  pointer-events: none;
}

.hide-scrollbar {
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.hide-scrollbar::-webkit-scrollbar {
  width: 0;
  height: 0;
  display: none
}
</style>