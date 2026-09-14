<template>
  <footer class="footer">
    <div class="footer-left">
      <p>© 2026 by Askar Abduvaliev.</p>
    </div>

    <div class="footer-right">
      <div class="contact-col">
        <h4>Телефон</h4>
        <p>+7 (995)-287-42-20</p>
      </div>
      <div class="contact-col">
        <h4>Почта</h4>
        <p>beqaskar@gmail.com</p>
      </div>
      <div class="contact-col">
        <SocialIcons />
      </div>
    </div>
  </footer>
</template>

<script setup>
import SocialIcons from './SocialIcons.vue'
</script>

<style scoped>
.footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 40px;
  background-color: var(--bg);
  font-size: 12px;
  flex-grow: 0;
  border-top: 1px solid var(--border);
  transition: background-color 0.4s ease, border-color 0.4s ease;
}

.footer-left p {
  margin: 0;
  color: var(--text);
  line-height: 1.2;
}

.footer-right {
  display: flex;
  gap: 60px;
  text-align: center;
  align-items: center;
}

.contact-col h4 {
  font-size: 12px;
  margin: 0 0 2px 0;
  font-weight: bold;
  color: var(--text);
}

.contact-col p {
  margin: 0;
  line-height: 1.2;
  color: var(--text);
}

.footer-right :deep(.socials) {
  background-color: transparent;
  padding: 0;
  border-radius: 0;
  gap: 14px;
}

.footer-right :deep(.social-link) {
  color: var(--text);
}

.footer-right :deep(.social-link:hover) {
  color: var(--accent);
}

@media (max-width: 768px) {
  .footer {
    flex-direction: column;
    gap: 16px;
    padding: 20px 20px;
    text-align: center;
  }

  .footer-right {
    flex-direction: column;
    gap: 16px;
  }

  .contact-col h4 {
    font-size: 11px;
  }

  .contact-col p {
    font-size: 12px;
  }
}

@media (max-width: 480px) {
  .footer {
    padding: 16px 14px;
    gap: 12px;
  }

  .footer-left p {
    font-size: 11px;
  }

  .footer-right {
    gap: 12px;
  }

  .contact-col h4 {
    font-size: 10px;
  }

  .contact-col p {
    font-size: 11px;
  }
}
</style>