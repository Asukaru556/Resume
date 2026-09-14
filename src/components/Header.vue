<!-- src/components/Header.vue -->
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
  flex-shrink: 0;
}

.name {
  font-weight: bold;
  font-size: 16px;
  color: var(--text);
  white-space: nowrap;
}

.separator {
  color: var(--text-muted);
}

.role {
  letter-spacing: 1px;
  color: var(--text);
  white-space: nowrap;
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
  white-space: nowrap;
}

.nav-link:hover {
  color: var(--accent);
}

.nav-link.router-link-active {
  color: var(--accent);
}

@media (max-width: 768px) {
  .header {
    padding: 12px 20px;
    gap: 12px;
  }

  .logo-area {
    gap: 8px;
    font-size: 12px;
  }

  .name {
    font-size: 13px;
  }

  .role,
  .separator {
    display: none;
  }

  .header-right {
    gap: 12px;
  }

  .navigation {
    gap: 14px;
  }

  .nav-link {
    font-size: 11px;
    letter-spacing: 0.5px;
  }
}

@media (max-width: 480px) {
  .header {
    padding: 10px 14px;
  }

  .logo-icon {
    width: 11px;
    height: 11px;
  }

  .name {
    font-size: 12px;
  }

  .navigation {
    gap: 10px;
  }

  .nav-link {
    font-size: 10px;
  }
}
</style>