<template>
  <v-app>
    <!-- Навигационная панель -->
    <v-app-bar color="primary" dark>
      <v-app-bar-title>
        <v-icon start>mdi-vuejs</v-icon>
        Ваш гид в Швейцарии
      </v-app-bar-title>
      
      <v-spacer></v-spacer>
      
      <v-btn icon @click="toggleTheme">
        <v-icon>{{ theme.global.current.value.dark ? 'mdi-weather-sunny' : 'mdi-weather-night' }}</v-icon>
      </v-btn>
      
      <v-chip color="secondary" variant="outlined">
        <v-icon start>mdi-clock</v-icon>
        {{ currentTime }}
      </v-chip>
    </v-app-bar>

    <!-- Основной контент -->
    <v-main>
      <v-container fluid>
        <v-row>
          <v-col cols="12">
            <v-card>
              <v-card-title class="text-h4">
                <v-icon start color="primary">mdi-rocket-launch</v-icon>
                Страничка гида в Швейцарии
              </v-card-title>
              
              <v-card-text>
                <v-alert type="success" variant="tonal" class="mb-4">
                  <template v-slot:prepend>
                    <v-icon>mdi-check-circle</v-icon>
                  </template>
                  <strong>{{ message }}</strong>
                  <br>
                  Ваш проект успешно настроен с Vue3 Composition API, Vuetify и Tailwind CSS
                </v-alert>
                
                
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { useTheme } from 'vuetify';
import CounterComponent from './CounterComponent.vue';
import TodoComponent from './TodoComponent.vue';
import HybridExample from './HybridExample.vue';

// Используем тему Vuetify
const theme = useTheme();

// Реактивные данные
const message = ref('Добро пожаловать в Symfony приложение с Vue3 Composition API, Vuetify и Tailwind CSS!');
const currentTime = ref('');

// Данные для списков
const features = ref([
  'Symfony 7.4',
  'PHP 8.4 с FPM',
  'Nginx веб-сервер',
  'PostgreSQL 16',
  'Redis для кэширования',
  'MailHog для тестирования email',
  'Doctrine ORM',
  'Vue3 Composition API',
  'Vuetify Material Design',
  'Tailwind CSS',
  'Vite',
]);

const commands = ref([
  {
    title: 'Запуск контейнеров',
    code: 'docker-compose up -d',
  },
  {
    title: 'Установка PHP зависимостей',
    code: 'docker-compose exec php composer install',
  },
  {
    title: 'Установка Node.js зависимостей',
    code: 'npm install',
  },
  {
    title: 'Сборка Vue компонентов',
    code: 'npm run dev',
  },
]);

// Таймер для обновления времени
let timer = null;

// Обновление времени
const updateTime = () => {
  currentTime.value = new Date().toLocaleTimeString('ru-RU');
};

// Переключение темы
const toggleTheme = () => {
  theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark';
};

// Хуки жизненного цикла
onMounted(() => {
  updateTime();
  timer = setInterval(updateTime, 1000);
});

onUnmounted(() => {
  if(timer) {
    clearInterval(timer);
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style> 