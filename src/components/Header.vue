<script setup>
import ThemeToggle from './ThemeToggle.vue'
</script>

<template>
  <header class="header">
    <RouterLink to="/" class="logo-area">
      <div class="logo-icon"></div>
      <span class="name">Abduvaliev Askar</span>
      <span class="separator">/</span>
      <span class="role">Frontend-Developer</span>
    </RouterLink>

    <div class="header-right">
      <nav class="navigation">
        <RouterLink to="/" class="nav-link">ГЛАВНАЯ</RouterLink>
        <RouterLink to="/projects" class="nav-link">ПРОЕКТЫ</RouterLink>
      </nav>
      <ThemeToggle />
    </div>
  </header>
</template>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 40px;
  background-color: var(--bg);
  transition: background-color 0.4s ease;
}

.logo-area {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 14px;
  text-decoration: none;
  color: var(--text);
}

.logo-icon {
  width: 14px;
  height: 14px;
  background-color: var(--accent);
  border-radius: 50%;
  transition: background-color 0.4s ease;
}

.name {
  font-weight: bold;
  font-size: 16px;
  color: var(--text);
}

.separator {
  color: var(--text-muted);
}

.role {
  letter-spacing: 1px;
  color: var(--text);
}

.header-right {
  display: flex;
  align-items: center;
  gap: 25px;
}

.navigation {
  display: flex;
  gap: 25px;
}

.nav-link {
  text-decoration: none;
  color: var(--text);
  font-size: 13px;
  letter-spacing: 1px;
  transition: color 0.3s;
  padding: 4px 0;
  position: relative;
}

.nav-link:hover {
  color: var(--accent);
}

.nav-link.router-link-active {
  color: var(--accent);
}
</style>