<template>
  <div :class="theme">
    <header class="text-center mb-4">
    </header>
    <Weather />
    <button @click="toggleTheme" class="theme-toggle-btn" :class="theme">Сменить тему</button>
  </div>
</template>

<script>
import Weather from './components/WeatherApp.vue';

export default {
  components: {
    Weather,
  },
  data() {
    return {
      theme: 'light-theme', // Начальная тема
    };
  },
  methods: {
    toggleTheme() {
      this.theme = this.theme === 'light-theme' ? 'dark-theme' : 'light-theme';
      document.body.className = this.theme; // Применяем тему к body
    },
  },
};
</script>

<style src="./styles.css"></style>

<style>
.theme-toggle-btn {
  position: fixed; /* Фиксированное положение */
  top: 20px; /* Отступ сверху */
  right: 20px; /* Отступ справа */
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>
