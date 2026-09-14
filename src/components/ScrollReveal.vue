<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  delay: { type: Number, default: 0 },
  distance: { type: Number, default: 60 },
  duration: { type: Number, default: 800 }
})

const el = ref(null)
const isVisible = ref(false)
let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          setTimeout(() => {
            isVisible.value = true
          }, props.delay)
          observer.unobserve(entry.target)
        }
      })
    },
    {
      threshold: 0.15,
      rootMargin: '0px 0px -50px 0px'
    }
  )

  if (el.value) observer.observe(el.value)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<template>
  <div
    ref="el"
    class="scroll-reveal"
    :class="{ visible: isVisible }"
    :style="{
      '--reveal-distance': distance + 'px',
      '--reveal-duration': duration + 'ms'
    }"
  >
    <slot />
  </div>
</template>

<style scoped>
.scroll-reveal {
  opacity: 0;
  transform: translateY(var(--reveal-distance));
  transition:
    opacity var(--reveal-duration) cubic-bezier(0.22, 1, 0.36, 1),
    transform var(--reveal-duration) cubic-bezier(0.22, 1, 0.36, 1);
  will-change: opacity, transform;
}

.scroll-reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
</style>