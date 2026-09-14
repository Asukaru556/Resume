<script setup>
defineProps({
  title: { type: String, required: true },
  description: { type: String, required: true },
  image: { type: String, required: true },
  tags: { type: Array, default: () => [] },
  link: { type: String, default: '#' }
})
</script>

<template>
  <a :href="link" class="project-card" target="_blank" rel="noopener">
    <div class="project-image-wrapper">
      <img :src="image" :alt="title" class="project-image" />
    </div>

    <div class="project-body">
      <h3 class="project-title">{{ title }}</h3>
      <p class="project-description">{{ description }}</p>

      <div v-if="tags.length" class="project-tags">
        <span v-for="tag in tags" :key="tag" class="project-tag">{{ tag }}</span>
      </div>

      <span class="project-link">
        Посмотреть проект
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="5" y1="12" x2="19" y2="12"></line>
          <polyline points="12 5 19 12 12 19"></polyline>
        </svg>
      </span>
    </div>
  </a>
</template>

<style scoped>
.project-card {
  display: flex;
  flex-direction: column;
  background-color: var(--bg-secondary);
  border-radius: 16px;
  overflow: hidden;
  text-decoration: none;
  color: var(--text);
  box-shadow: var(--shadow);
  border: 1px solid var(--card-border);
  transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease;
  height: 100%;
}

.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
  border-color: var(--accent);
}

.project-image-wrapper {
  width: 100%;
  aspect-ratio: 16 / 10;
  overflow: hidden;
  background-color: var(--bg);
}

.project-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s ease;
}

.project-card:hover .project-image {
  transform: scale(1.05);
}

.project-body {
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  flex: 1;
}

.project-title {
  font-size: 20px;
  font-weight: bold;
  margin: 0;
  color: var(--text);
}

.project-description {
  font-size: 14px;
  line-height: 1.5;
  color: var(--text-muted);
  margin: 0;
  flex: 1;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.project-tag {
  font-size: 11px;
  padding: 4px 10px;
  border-radius: 12px;
  background-color: rgba(255, 165, 30, 0.12);
  color: var(--accent);
  letter-spacing: 0.5px;
  font-weight: 600;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 13px;
  font-weight: 600;
  color: var(--accent);
  margin-top: 4px;
  transition: gap 0.3s ease;
}

.project-card:hover .project-link {
  gap: 10px;
}

@media (max-width: 480px) {
  .project-body {
    padding: 14px;
    gap: 8px;
  }

  .project-title {
    font-size: 16px;
  }

  .project-description {
    font-size: 12px;
  }

  .project-tag {
    font-size: 10px;
    padding: 3px 8px;
  }

  .project-link {
    font-size: 12px;
  }
}
</style>