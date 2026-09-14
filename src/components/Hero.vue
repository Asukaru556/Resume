<template>
  <section class="hero-section">
    <div class="hero-left">
      <div class="beige-background"></div>

      <div class="profile-card">
        <div class="card-content">
          <div class="avatar-container">
            <img
              v-for="(photo, index) in photos"
              :key="index"
              :src="photo"
              alt="Askar Abduvaliev"
              class="avatar"
              :class="{ 'active': index === currentIndex }"
            />
          </div>
          <h2 class="card-name">Askar<br>Abduvaliev</h2>
          <div class="blue-line"></div>
          <p class="card-role">Frontend-Developer</p>
        </div>

        <SocialIcons />
      </div>
    </div>

    <div class="hero-right">
      <h1 class="greeting">Привет!</h1>
      <p class="subtitle">Здесь вы узнаете кто я и чем занимаюсь</p>

      <div class="buttons">
        <RouterLink to="/projects" class="btn btn-primary">ПРОЕКТЫ</RouterLink>
      </div>

      <div class="description">
        <p>Меня зовут Аскар, я студент 3 курса направления frontend-разработчик. Специализируюсь на создании пользовательских интерфейсов на Vue 3, React. В работе использую JavaScript/TypeScript, Pinia, Vue Router, Vite, REST API и Git.</p>
        <p>Мне важно, чтобы код был не только рабочим, но и понятным, а интерфейс — быстрым и удобным для пользователя. Легко нахожу общий язык с командой, беру ответственность за задачи и постоянно учусь новому.</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import SocialIcons from './SocialIcons.vue'

const photos = [
  '/public/ava/5269718787236240676.jpg',
  '/public/ava/5269718787236240677.jpg',
  '/public/ava/5269718787236240678.jpg'
]

const currentIndex = ref(0)

let intervalId = null

const nextPhoto = () => {
  currentIndex.value = (currentIndex.value + 1) % photos.length
}

onMounted(() => {
  photos.forEach(src => {
    const img = new Image()
    img.src = src
  })

  intervalId = setInterval(nextPhoto, 5000)
})

onUnmounted(() => {
  clearInterval(intervalId)
})
</script>

<style scoped>
.hero-section {
  display: flex;
  flex: 1;
  width: 100%;
  background-color: var(--bg);
}

.hero-left {
  flex: 1;
  position: relative;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.beige-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url('/images/bg-bg.png');
  border-radius: 5ch;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  z-index: 1;
}

.profile-card {
  position: relative;
  z-index: 2;
  width: 320px;
  background-color: var(--bg-secondary);
  margin-right: -50px;
  box-shadow: var(--shadow);
  display: flex;
  flex-direction: column;
  transition: background-color 0.4s ease, box-shadow 0.4s ease;
  border-radius: 5ch;
  border: 1px solid var(--card-border);
}

.card-content {
  padding: 40px 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.avatar-container {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  overflow: hidden;
  margin-bottom: 20px;
  background-color: #ccc;
  position: relative;
  border: 3px solid var(--accent);
  box-shadow:
    0 0 20px 3px rgba(255, 165, 30, 0.5),
    0 0 40px 8px rgba(255, 165, 30, 0.2);
  transition: box-shadow 0.4s ease, border-color 0.4s ease;
}

.avatar {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0;
  transform: scale(1.1);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.avatar.active {
  opacity: 1;
  transform: scale(1);
  z-index: 2;
}

.card-name {
  font-size: 24px;
  text-align: center;
  line-height: 1.2;
  margin-bottom: 15px;
  font-weight: bold;
  color: var(--text);
}

.blue-line {
  width: 30px;
  height: 2px;
  background-color: var(--accent);
  margin-bottom: 15px;
}

.card-role {
  font-size: 12px;
  letter-spacing: 2px;
  color: var(--text);
}

.hero-right {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 40px 10% 40px 80px;
  gap: 20px;
}

.greeting {
  font-size: 64px;
  font-weight: 900;
  line-height: 1.1;
  margin: 0 0 5px 0;
  color: var(--text);
}

.subtitle {
  font-size: 18px;
  margin: 0 0 10px 0;
  color: var(--text);
}

.buttons {
  display: flex;
  gap: 15px;
  margin-bottom: 10px;
}

.btn {
  padding: 12px 30px;
  border-radius: 25px;
  font-size: 12px;
  font-weight: bold;
  cursor: pointer;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.btn-primary {
  background-color: var(--accent);
  color: #ffffff;
  border: none;
}

.btn-primary:hover {
  background-color: var(--text);
  color: var(--bg);
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(255, 165, 30, 0.35);
}

.btn-primary:active {
  transform: translateY(0);
}

.description p {
  font-size: 14px;
  line-height: 1.6;
  color: var(--text-muted);
  margin: 0 0 15px 0;
}

@media (max-width: 1024px) {
  .hero-right {
    padding: 40px 6% 40px 60px;
  }

  .greeting {
    font-size: 52px;
  }
}

@media (max-width: 900px) {
  .hero-section {
    flex-direction: column;
  }

  .hero-left {
    flex: none;
    width: 100%;
    min-height: 380px;
    justify-content: center;
    padding: 30px 0;
  }

  .beige-background {
    border-radius: 0;
  }

  .profile-card {
    margin-right: 0;
    width: 280px;
  }

  .hero-right {
    flex: none;
    width: 100%;
    padding: 40px 24px;
    align-items: center;
    text-align: center;
  }

  .greeting {
    font-size: 44px;
  }

  .subtitle {
    font-size: 16px;
  }

  .description p {
    font-size: 14px;
  }

  .buttons {
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .hero-left {
    min-height: 340px;
    padding: 20px 0;
  }

  .profile-card {
    width: 240px;
  }

  .card-content {
    padding: 30px 16px;
  }

  .avatar-container {
    width: 120px;
    height: 120px;
    margin-bottom: 15px;
  }

  .card-name {
    font-size: 20px;
  }

  .card-role {
    font-size: 11px;
    letter-spacing: 1.5px;
  }

  .hero-right {
    padding: 30px 18px;
    gap: 16px;
  }

  .greeting {
    font-size: 34px;
  }

  .subtitle {
    font-size: 14px;
  }

  .description p {
    font-size: 13px;
  }

  .btn {
    padding: 10px 24px;
    font-size: 11px;
  }
}
</style>