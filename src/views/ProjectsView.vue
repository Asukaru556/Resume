<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const projects = [
  {
    id: 1,
    title: 'MuselFarm',
    type: 'Практика в компании',
    subtitle: 'Full-Stack система управления мидийной фермой',
    description: 'Разработал с нуля full-stack систему для автоматизации и мониторинга процессов на мидийной ферме. Проект охватывает управление инфраструктурой, учёт биомассы и сбор телеметрии с датчиков. Реализована JWT-авторизация с ролевой моделью, REST API с документацией Swagger и адаптивный SPA-интерфейс.',
    image: '/projects/muselfarm.jpg',
    tags: ['NestJS', 'TypeScript', 'Prisma', 'PostgreSQL', 'Vue 3', 'Docker', 'JWT'],
    link: 'https://github.com/Asukaru556/MuselFarm-Frontend',
    linkLabel: 'Frontend',
    link2: 'https://github.com/Asukaru556/MuselFarm-Backend',
    link2Label: 'Backend'
  },
  {
    id: 2,
    title: 'NeOdin LMS',
    type: 'Пет-проект',
    subtitle: 'Система управления обучением для студентов и преподавателей',
    description: 'Full-stack LMS-платформа с разделением ролей: студенты просматривают курсы, задания, оценки и расписание; учителя управляют курсами, создают уроки, проверяют ответы и выставляют оценки. Реализована JWT-аутентификация, защищённые маршруты и seed-скрипт для быстрого наполнения БД тестовыми данными.',
    image: '/projects/neodin.jpg',
    tags: ['Vue 3', 'Quasar', 'Pinia', 'Node.js', 'Express', 'Sequelize', 'MySQL', 'JWT'],
    link: 'https://github.com/Asukaru556/NeOdin_LMS',
    linkLabel: 'Frontend',
    link2: 'https://github.com/Asukaru556/NeOdin_LMS-Backend',
    link2Label: 'Backend'
  },
  {
    id: 3,
    title: 'ZenPulse',
    type: 'Тестовое задание',
    subtitle: 'Мобильное приложение на React Native (Expo)',
    description: 'Разработал мобильное приложение на React Native (Expo) в рамках тестового задания для компании ZenPulse. Основная задача — создать адаптивный интерфейс, который корректно отображается на устройствах с разными размерами экрана (от iPhone SE до Pro Max). Использовал ИИ-ассистентов для ускорения разработки и отладки, контролировал качество через тестирование на эмуляторах.',
    image: '/projects/Zenpulse.jpg',
    tags: ['React Native', 'Expo', 'TypeScript', 'NativeWind', 'Expo Router', 'Reanimated'],
    link: 'https://github.com/Asukaru556/AIProject_ZenPulse',
    linkLabel: 'Исходный код'
  },
  {
    id: 4,
    title: 'AllTeemStroy',
    type: 'Заказ',
    subtitle: 'Лендинг для архитектурно-строительной компании',
    description: 'Разработал одностраничный сайт-визитку для строительной компании ALL TEEM STROY на чистом HTML, CSS и JavaScript. Реализовал анимированные счётчики, 3D-эффект карточек услуг при наведении, кастомный слайдер и scroll-reveal анимации через Intersection Observer. Адаптивная навигация с burger-меню для мобильных устройств.',
    image: '/projects/allteemstroy.jpg',
    tags: ['HTML5', 'CSS3', 'JavaScript', 'Intersection Observer', 'Адаптивная вёрстка'],
    link: 'https://www.allteemstroy.uz/',
    linkLabel: 'Сайт'
  },
  {
    id: 5,
    title: 'Portfolio Website',
    type: 'Пет-проект',
    subtitle: 'Персональный сайт-портфолио на Vue 3',
    description: 'Разработал SPA-портфолио с нуля на Vue 3 и Vue Router. Реализовал переключатель тёмной и светлой темы через CSS-переменные с сохранением в localStorage, sticky-scroll навигацию по проектам с раздельными анимациями текста и фото, плавные переходы между страницами через Transition с режимом out-in, автоматическую смену фотографий профиля каждые 5 секунд, кастомный фон секции с анимацией и полностью адаптивную вёрстку под мобильные устройства.',
    image: '/projects/resume.jpg',
    tags: ['Vue 3', 'Vue Router', 'Vite', 'CSS Variables', 'Transition', 'IntersectionObserver', 'LocalStorage'],
    link: 'https://github.com/Asukaru556/Resume',
    linkLabel: 'Исходный код'
  }
]

const typeStyles = {
  'Практика':    { bg: 'rgba(30, 94, 255, 0.12)',  color: '#1e5eff' },
  'Пет-проект':  { bg: 'rgba(139, 92, 246, 0.12)', color: '#8b5cf6' },
  'Заказ':       { bg: 'rgba(16, 185, 129, 0.12)', color: '#10b981' }
}

const getTypeStyle = (type) => typeStyles[type] || typeStyles['Пет-проект']

const SLIDE_SCROLL = 0.5

const activeIndex = ref(0)
const container = ref(null)

const sectionHeight = computed(() => {
  return `calc(100vh + ${(projects.length - 1) * SLIDE_SCROLL * 100}vh)`
})

const updateIndex = () => {
  if (!container.value) return
  const rect = container.value.getBoundingClientRect()
  const scrolled = Math.max(0, -rect.top)
  const slideHeight = window.innerHeight * SLIDE_SCROLL
  const index = Math.round(scrolled / slideHeight)
  activeIndex.value = Math.max(0, Math.min(projects.length - 1, index))
}

const scrollToProject = (i) => {
  if (!container.value) return
  const slideHeight = window.innerHeight * SLIDE_SCROLL
  const top = container.value.offsetTop + i * slideHeight
  window.scrollTo({ top, behavior: 'smooth' })
}

onMounted(() => {
  window.addEventListener('scroll', updateIndex, { passive: true })
  window.addEventListener('resize', updateIndex)
  updateIndex()
})

onUnmounted(() => {
  window.removeEventListener('scroll', updateIndex)
  window.removeEventListener('resize', updateIndex)
})
</script>

<template>
  <section
    ref="container"
    class="projects-page"
    :style="{ height: sectionHeight }"
  >
    <div class="projects-sticky">
      <div class="project-info-layer">
        <Transition name="fade-info" mode="out-in">
          <div class="project-info" :key="activeIndex">
            <span class="project-counter">
              {{ String(activeIndex + 1).padStart(2, '0') }}
              <span class="counter-divider">/</span>
              {{ String(projects.length).padStart(2, '0') }}
            </span>

            <h2 class="project-title">{{ projects[activeIndex].title }}</h2>

            <span
              class="project-type"
              :style="{
                backgroundColor: getTypeStyle(projects[activeIndex].type).bg,
                color: getTypeStyle(projects[activeIndex].type).color
              }"
            >
              {{ projects[activeIndex].type }}
            </span>

            <p class="project-subtitle">{{ projects[activeIndex].subtitle }}</p>

            <p class="project-description">{{ projects[activeIndex].description }}</p>

            <div class="project-tags">
              <span
                v-for="tag in projects[activeIndex].tags"
                :key="tag"
                class="project-tag"
              >
                {{ tag }}
              </span>
            </div>

            <div class="project-links">
              <a
                :href="projects[activeIndex].link"
                target="_blank"
                rel="noopener"
                class="project-link"
              >
                {{ projects[activeIndex].linkLabel || 'Посмотреть проект' }}
                <svg
                  width="16" height="16" viewBox="0 0 24 24"
                  fill="none" stroke="currentColor" stroke-width="2"
                  stroke-linecap="round" stroke-linejoin="round"
                >
                  <line x1="5" y1="12" x2="19" y2="12"></line>
                  <polyline points="12 5 19 12 12 19"></polyline>
                </svg>
              </a>

              <a
                v-if="projects[activeIndex].link2"
                :href="projects[activeIndex].link2"
                target="_blank"
                rel="noopener"
                class="project-link"
              >
                {{ projects[activeIndex].link2Label || 'Ссылка' }}
                <svg
                  width="16" height="16" viewBox="0 0 24 24"
                  fill="none" stroke="currentColor" stroke-width="2"
                  stroke-linecap="round" stroke-linejoin="round"
                >
                  <line x1="5" y1="12" x2="19" y2="12"></line>
                  <polyline points="12 5 19 12 12 19"></polyline>
                </svg>
              </a>
            </div>
          </div>
        </Transition>
      </div>

      <div class="project-cards-layer">
        <div
          class="cards-track"
          :style="{ transform: `translateY(-${activeIndex * 100}%)` }"
        >
          <div
            v-for="p in projects"
            :key="p.id"
            class="card-slide"
          >
            <div class="project-card">
              <img :src="p.image" :alt="p.title" class="project-image" />
              <div class="card-overlay">
                <span
                  class="card-type-badge"
                  :style="{
                    backgroundColor: getTypeStyle(p.type).bg,
                    color: getTypeStyle(p.type).color
                  }"
                >
                  {{ p.type }}
                </span>
                <span class="card-label">{{ p.title }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="indicators">
        <button
          v-for="(p, i) in projects"
          :key="p.id"
          class="indicator"
          :class="{ active: i === activeIndex }"
          @click="scrollToProject(i)"
          :aria-label="`Перейти к проекту ${i + 1}`"
        />
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects-page {
  position: relative;
  background-color: var(--bg);
}

.projects-sticky {
  position: sticky;
  top: 0;
  height: 100vh;
  display: flex;
  align-items: stretch;
  overflow: hidden;
}

.project-info-layer {
  flex: 1;
  height: 100vh;
  display: flex;
  align-items: center;
  padding-left: 8%;
  padding-right: 4%;
  box-sizing: border-box;
}

.project-info {
  max-width: 700px;
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.project-counter {
  font-size: 13px;
  letter-spacing: 2px;
  color: var(--text-muted);
  font-weight: 600;
}

.counter-divider {
  opacity: 0.4;
  margin: 0 4px;
}

.project-title {
  font-size: 48px;
  font-weight: 900;
  line-height: 1.1;
  color: var(--text);
  margin: 0;
}

.project-type {
  display: inline-flex;
  align-items: center;
  align-self: flex-start;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.2px;
  text-transform: uppercase;
  padding: 5px 12px;
  border-radius: 20px;
  margin-top: -4px;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.project-subtitle {
  font-size: 15px;
  font-weight: 600;
  color: var(--accent);
  margin: 4px 0 0 0;
  letter-spacing: 0.3px;
}

.project-description {
  font-size: 15px;
  line-height: 1.6;
  color: var(--text-muted);
  margin: 0;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-top: 4px;
}

.project-tag {
  font-size: 12px;
  padding: 5px 12px;
  border-radius: 12px;
  background-color: rgba(213, 216, 21, 0.349);
  color: var(--accent);
  letter-spacing: 0.5px;
  font-weight: 600;
}

.project-links {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  margin-top: 8px;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 600;
  color: var(--accent);
  text-decoration: none;
  transition: gap 0.3s ease;
}

.project-link:hover {
  gap: 14px;
}

.fade-info-enter-active,
.fade-info-leave-active {
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.fade-info-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.fade-info-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

.project-cards-layer {
  flex: 1;
  height: 100vh;
  overflow: hidden;
  position: relative;
}

.cards-track {
  display: flex;
  flex-direction: column;
  height: 100%;
  transition: transform 0.85s cubic-bezier(0.65, 0, 0.35, 1);
  will-change: transform;
}

.card-slide {
  height: 100vh;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 60px;
  box-sizing: border-box;
}

.project-card {
  position: relative;
  width: 100%;
  max-width: 1000px;
  aspect-ratio: 4 / 3;
  border-radius: 20px;
  overflow: hidden;
  background-color: var(--bg-secondary);
  border: 2px solid var(--accent);
  box-shadow: 0 0 30px 4px rgba(255, 165, 30, 0.35);
  transition: box-shadow 0.4s ease, border-color 0.4s ease, transform 0.4s ease;
}

.project-card:hover {
  border-color: var(--accent);
  box-shadow: 0 0 50px 8px rgba(255, 165, 30, 0.55);
  transform: translateY(-4px);
}

.project-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.8s ease;
}

.project-card:hover .project-image {
  transform: scale(1.05);
}

.card-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 20px 24px;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.75), transparent);
  pointer-events: none;
  display: flex;
  flex-direction: column;
  gap: 6px;
  align-items: flex-start;
}

.card-type-badge {
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 1.2px;
  text-transform: uppercase;
  padding: 4px 10px;
  border-radius: 12px;
}

.card-label {
  color: #ffffff;
  font-size: 18px;
  font-weight: 700;
  letter-spacing: 0.5px;
}

.indicators {
  position: absolute;
  right: 32px;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 12px;
  z-index: 10;
}

.indicator {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  border: 2px solid var(--text-muted);
  background: transparent;
  cursor: pointer;
  padding: 0;
  transition: all 0.3s ease;
}

.indicator:hover {
  border-color: var(--accent);
  transform: scale(1.2);
}

.indicator.active {
  background-color: var(--accent);
  border-color: var(--accent);
  transform: scale(1.3);
}

@media (max-width: 900px) {
  .projects-sticky {
    flex-direction: column-reverse;
  }

  .project-info-layer,
  .project-cards-layer {
    height: 50vh;
    flex: 0 0 50vh;
  }

  .project-info-layer {
    padding: 20px 6%;
    align-items: flex-start;
    overflow-y: auto;
  }

  .project-info {
    max-width: 100%;
    gap: 8px;
  }

  .project-title {
    font-size: 28px;
  }

  .project-type {
    font-size: 10px;
    padding: 4px 10px;
  }

  .project-subtitle {
    font-size: 13px;
  }

  .project-description {
    font-size: 13px;
  }

  .project-tag {
    font-size: 11px;
    padding: 4px 10px;
  }

  .card-slide {
    height: 50vh;
    padding: 20px 30px;
  }

  .indicators {
    right: 12px;
    top: auto;
    bottom: 20px;
    transform: none;
    flex-direction: row;
  }
}

@media (max-width: 480px) {
  .project-title {
    font-size: 22px;
  }

  .project-description {
    font-size: 12px;
    line-height: 1.5;
  }

  .project-subtitle {
    font-size: 12px;
  }

  .project-tag {
    font-size: 10px;
    padding: 3px 8px;
  }

  .project-link {
    font-size: 12px;
    gap: 6px;
  }

  .project-info-layer {
    padding: 12px 5%;
  }

  .card-slide {
    padding: 12px 20px;
  }

  .project-card {
    border-radius: 14px;
    box-shadow: 0 0 20px 3px rgba(255, 165, 30, 0.35);
  }

  .card-overlay {
    padding: 14px 16px;
  }

  .card-label {
    font-size: 15px;
  }

  .card-type-badge {
    font-size: 9px;
    padding: 3px 8px;
  }

  .indicators {
    right: 8px;
    bottom: 12px;
    gap: 8px;
  }

  .indicator {
    width: 8px;
    height: 8px;
  }
}
</style>