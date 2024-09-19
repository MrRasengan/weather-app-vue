<template>
  <div class="weather container mt-5">
		<h1>Смотри погоду в любом городе России!</h1>
    <h1>Погода в {{ city }}</h1>
    <div class="input-group mb-3">
      <input type="text" v-model="city" @keyup.enter="fetchWeather" class="form-control" placeholder="Введите название города" />
      <button @click="fetchWeather" class="btn btn-primary">Показать погоду</button>
    </div>

    <div v-if="weather" class="alert alert-info">
      <p>Температура: {{ weather.main.temp }}°C</p>
      <p>Состояние: {{ weather.weather[0].description }}</p>
    </div>
    <div v-if="error" class="alert alert-danger">{{ error }}</div>
    <div v-else-if="!weather && !error">
      <p>Загрузка...</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      city: 'Москва',
      weather: null,
      error: null,
    };
  },
  mounted() {
    this.fetchWeather();
  },
  methods: {
    async fetchWeather() {
      const apiKey = 'edef2f08f1ba0561fa8800768cb20f3c';
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${apiKey}`;
      this.error = null; // Сбрасываем ошибку перед новым запросом
      try {
        const response = await axios.get(url, { timeout: 10000 });
        this.weather = response.data;
      } catch (error) {
        this.error = 'Не удалось получить данные о погоде. Проверьте название города.';
        console.error('Ошибка при получении данных о погоде:', error);
      }
    },
  },
};
</script>

<style scoped>
.weather {
  text-align: center;
  margin-top: 20px;
}

input {
  padding: 10px;
  margin-right: 10px;
}

button {
  padding: 10px;
}

.error {
  color: red;
}
</style>


<!-- const apiKey = '5442c4f11b5855389cf8fed23dbd2ea9'; -->