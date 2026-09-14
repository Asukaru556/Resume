<script setup>
import { ref, watch, onMounted } from 'vue'

const isDark = ref(false)

const applyTheme = (dark) => {
  document.documentElement.setAttribute('data-theme', dark ? 'dark' : 'light')
  localStorage.setItem('theme', dark ? 'dark' : 'light')
}

const toggle = () => {
  isDark.value = !isDark.value
}

onMounted(() => {
  const saved = localStorage.getItem('theme')
  if (saved) {
    isDark.value = saved === 'dark'
  } else {
    isDark.value = window.matchMedia('(prefers-color-scheme: dark)').matches
  }
  applyTheme(isDark.value)
})

watch(isDark, (newVal) => {
  applyTheme(newVal)
})
</script>

<template>
  <button
    class="theme-toggle"
    @click="toggle"
    :title="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
    :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
  >
    <svg
      class="icon sun"
      :class="{ active: !isDark }"
      width="22" height="22" viewBox="0 0 24 24"
      fill="none" stroke="currentColor" stroke-width="2"
      stroke-linecap="round" stroke-linejoin="round"
    >
      <circle cx="12" cy="12" r="5"></circle>
      <line x1="12" y1="1" x2="12" y2="3"></line>
      <line x1="12" y1="21" x2="12" y2="23"></line>
      <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
      <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
      <line x1="1" y1="12" x2="3" y2="12"></line>
      <line x1="21" y1="12" x2="23" y2="12"></line>
      <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
      <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
    </svg>

    <svg
      class="icon moon"
      :class="{ active: isDark }"
      width="22" height="22" viewBox="0 0 24 24"
      fill="none" stroke="currentColor" stroke-width="2"
      stroke-linecap="round" stroke-linejoin="round"
    >
      <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
    </svg>
  </button>
</template>

<style scoped>
.theme-toggle {
  position: relative;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text);
  transition: background-color 0.3s ease, color 0.3s ease;
}

.theme-toggle:hover {
  background-color: rgba(30, 94, 255, 0.1);
  color: var(--accent);
}

.icon {
  position: absolute;
  transition: opacity 0.4s ease, transform 0.4s ease;
}

.icon.sun {
  opacity: 0;
  transform: rotate(-90deg) scale(0.5);
}

.icon.sun.active {
  opacity: 1;
  transform: rotate(0deg) scale(1);
}

.icon.moon {
  opacity: 0;
  transform: rotate(90deg) scale(0.5);
}

.icon.moon.active {
  opacity: 1;
  transform: rotate(0deg) scale(1);
}
</style>