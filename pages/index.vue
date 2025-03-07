<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const container = ref<HTMLElement | null>(null);

onMounted(() => {
  if (container.value) {
    gsap.to(container.value, {
      x: () => -(container.value!.scrollWidth - window.innerWidth),
      ease: 'none',
      scrollTrigger: {
        trigger: container.value,
        pin: true,
        scrub: 1,
        end: () => '+=' + (container.value!.scrollWidth - window.innerWidth),
      },
    });
  }
});
</script>

<template>
    <div ref="container" class="container">
    <Screen1 />
    <Screen2 />
    <Screen3 />
    <!-- Добавьте остальные экраны -->
  </div>
</template>

<style scoped>
.container {
  display: flex;
  width: max-content;
}

.screen {
  width: 100vw;
  height: 100vh;
  flex-shrink: 0;
}
</style>