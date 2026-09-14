<script setup>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="app-container">
    <Header />
    <main class="main-content">
      <RouterView v-slot="{ Component, route }">
        <Transition name="page-fade" mode="out-in" appear>
          <component :is="Component" :key="route.path" />
        </Transition>
      </RouterView>
    </main>
    <Footer />
  </div>
</template>

<style>
.app-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100%;
  background-color: var(--bg);
  transition: background-color 0.4s ease;
}

.main-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  width: 100%;
  position: relative;
  overflow: clip;  
}

.page-fade-leave-active {
  transition: opacity 0.4s ease, transform 0.4s ease;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  min-height: 100vh;
  z-index: 1;
}

.page-fade-leave-to {
  opacity: 0;
  transform: translateX(-60px);
}

.page-fade-enter-active {
  transition: opacity 0.5s ease, transform 0.5s ease;
  transition-delay: 0.1s;
  z-index: 2;
}

.page-fade-enter-from {
  opacity: 0;
  transform: translateX(60px);
}

@media (max-width: 768px) {
  .page-fade-leave-to {
    transform: translateX(-30px);
  }

  .page-fade-enter-from {
    transform: translateX(30px);
  }
}
</style>