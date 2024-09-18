<script setup lang="ts">
import DemoSimple from './components/demos/Simple.vue';
import DemoClassic from './components/demos/Classic.vue';
</script>

<template>
  <div class="max-w-[90em] mx-auto p-5">
    <h2 class="text-lg">Demo (Simple)</h2>
    <hr />
    <section class="p-5">
      <DemoSimple />
    </section>

    <h2 class="text-lg">Demo (Classic)</h2>
    <hr />
    <section class="p-5">
      <DemoClassic />
    </section>
  </div>
</template>