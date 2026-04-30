<template>
  <div class="min-h-screen w-full bg-black text-white selection:bg-white/10 font-sans overflow-x-hidden">
    <div class="relative h-full w-full">
      <!-- Фон с градиентами -->
      <div class="pointer-events-none absolute inset-0 bg-[radial-gradient(circle_at_top_left,_rgba(56,189,248,0.12),_transparent_30%),radial-gradient(circle_at_top_right,_rgba(96,165,250,0.08),_transparent_25%),radial-gradient(circle_at_bottom_left,_rgba(16,185,129,0.06),_transparent_28%)]" />
      
      <div class="relative mx-auto h-full w-full px-4 py-6 sm:px-6 lg:px-8 flex flex-col gap-6 max-w-7xl">
        
        <!-- Верхняя сетка: Профиль, Соцсети, Стек -->
        <div class="grid grid-cols-1 xl:grid-cols-[320px_1fr_320px] gap-6">
          
          <!-- Профиль -->
          <section class="flex flex-col justify-between rounded-3xl border border-[#1f1f1f] bg-[#141414] p-6 sm:p-8">
            <div>
              <div class="flex items-start justify-between gap-4">
                <div class="flex h-12 w-12 items-center justify-center rounded-full bg-[#1c1c1c] border border-[#2d2d2d] text-lg font-bold text-sky-400">
                  <img 
                  src="/content/avatar.png" 
                  alt="Profile Image"
                  class="h-full w-full object-cover rounded-full"
                  >
                </div>
                <div class="rounded-full bg-[#1c1c1c] px-4 py-2 text-[10px] sm:text-xs text-gray-400 border border-[#2d2d2d]">Frontend-разработчик</div>
              </div>
              <div class="mt-12">
                <h1 class="text-3xl sm:text-4xl font-extrabold tracking-tight">Матвей<br/>Тузиков</h1>
                <p class="mt-4 text-gray-400 text-sm leading-relaxed">Студент-программист. Специализируюсь на Vue.js и автоматизации на Python.</p>
              </div>
            </div>
            <div class="mt-8 space-y-2 text-[10px] text-gray-500 uppercase tracking-wider">
              <p>📍 Тюмень, Россия</p>
              <p>💻 Чистый код и UI/UX</p>
            </div>
          </section>

          <!-- Центр: Соцсети и Резюме -->
          <div class="grid grid-cols-1 gap-6">
            <section class="rounded-3xl border border-[#1f1f1f] bg-[#141414] p-6 sm:p-8">
              <div class="flex items-center justify-between mb-6">
                <h2 class="text-xl sm:text-2xl font-bold tracking-tight">Связаться со мной</h2>
                <span class="text-[9px] text-gray-600 uppercase tracking-[0.2em]">Контакты</span>
              </div>
              <div class="grid grid-cols-3 gap-3">
                <a 
                  v-for="item in socials" 
                  :key="item.name" 
                  :href="item.href" 
                  target="_blank"
                  rel="noopener noreferrer"
                  class="group flex flex-col items-center justify-center py-5 rounded-2xl border border-[#262626] bg-[#1c1c1c] transition-all hover:border-sky-500/50 hover:bg-[#1f1f1f]"
                  >
                <div class="w-6 h-6 mb-2 text-gray-400 group-hover:text-white transition-colors" v-html="item.svg"></div>
                  <span class="text-[9px] text-gray-500 uppercase group-hover:text-white transition-colors">{{ item.name }}</span>
                  </a>
              </div>                          
            </section>
            <section class="rounded-3xl border border-[#1f1f1f] bg-[#141414] p-6 sm:p-8 flex flex-col justify-between">
              <h2 class="text-xl sm:text-2xl font-bold tracking-tight text-white">Мое резюме</h2>
              <button class="mt-6 w-full inline-flex items-center justify-center rounded-xl bg-white px-6 py-4 text-sm font-bold text-black transition hover:bg-sky-400">Скачать CV</button>
            </section>
          </div>

          <!-- Стек технологий -->
          <section class="rounded-3xl border border-[#1f1f1f] bg-[#141414] p-6 sm:p-8">
            <h2 class="text-xl sm:text-2xl font-bold tracking-tight mb-8">Технологии</h2>
            <div class="grid grid-cols-1 gap-3">
              <div v-for="tech in stack" :key="tech.name" class="flex items-center gap-4 rounded-xl border border-[#262626] bg-[#1c1c1c] px-4 py-3 hover:border-sky-500/30 transition-all group">
                <div class="flex h-10 w-10 shrink-0 items-center justify-center rounded-lg bg-[#262626] border border-[#333333] group-hover:bg-sky-500/10 group-hover:border-sky-500/50 transition-all">
                  <div class="w-5 h-5 text-gray-400 group-hover:text-white transition-colors" v-html="tech.svg"></div>
                </div>
                <span class="font-semibold text-gray-300 text-sm group-hover:text-white transition-colors">{{ tech.name }}</span>
              </div>
            </div>
          </section>
        </div>

        <!-- Нижний блок: Проекты -->
        <section class="rounded-3xl border border-[#1f1f1f] bg-[#141414] p-6 sm:p-8 shadow-2xl">
          <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between mb-8 gap-4">
            <h2 class="text-2xl sm:text-3xl font-extrabold tracking-tight">Мои работы</h2>
            <button 
              @click="showFullList = !showFullList"
              class="rounded-full border border-[#262626] bg-[#1c1c1c] px-6 py-2 text-[10px] text-gray-400 font-bold hover:text-white hover:border-sky-500/50 transition-all uppercase"
            >
              {{ showFullList ? 'Свернуть' : 'Все проекты' }}
            </button>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
            <article 
              v-for="project in visibleProjects" 
              :key="project.title" 
              @click="openProject(project)"
              class="group rounded-2xl border border-[#262626] bg-[#1c1c1c] p-6 transition-all hover:border-sky-500/30 hover:bg-[#1f1f1f] cursor-pointer"
            >
              <div class="flex justify-between items-start mb-4">
                <h3 class="text-lg font-bold text-gray-100 group-hover:text-sky-400 transition-colors">{{ project.title }}</h3>
                <svg class="text-gray-700 group-hover:text-sky-400 transition-all transform group-hover:translate-x-1 group-hover:-translate-y-1" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="7" y1="17" x2="17" y2="7"></line><polyline points="7 7 17 7 17 17"></polyline></svg>
              </div>
              <p class="text-sm text-gray-500 leading-relaxed">{{ project.desc }}</p>
            </article>
          </div>
        </section>
      </div>
    </div>

    <!-- Модальное окно -->
    <Transition name="fade">
      <div v-if="selectedProject" class="fixed inset-0 z-50 flex items-center justify-center p-4">
        <div class="absolute inset-0 bg-black/80 backdrop-blur-md" @click="closeModal"></div>
        
        <div class="relative w-full max-w-2xl rounded-3xl border border-[#2d2d2d] bg-[#141414] shadow-2xl overflow-hidden">
          <div class="w-full h-48 sm:h-64 overflow-hidden border-b border-[#2d2d2d] bg-[#0a0a0a]">
            <img :src="selectedProject.image" :alt="selectedProject.title" class="w-full h-full object-cover opacity-80">
          </div>

          <div class="p-6 sm:p-8">
            <div class="flex justify-between items-start mb-6">
              <div>
                <h2 class="text-2xl sm:text-3xl font-bold text-white">{{ selectedProject.title }}</h2>
                <div class="flex flex-wrap gap-2 mt-3">
                  <span v-for="tag in selectedProject.tags" :key="tag" class="text-[9px] px-2 py-1 rounded-full bg-sky-500/10 border border-sky-500/20 text-sky-400 uppercase font-bold tracking-wider">{{ tag }}</span>
                </div>
              </div>
              <button @click="closeModal" class="text-gray-500 hover:text-white transition-colors">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
              </button>
            </div>
            
            <div class="prose prose-invert max-w-none">
              <p class="text-gray-400 leading-relaxed text-sm sm:text-base">{{ selectedProject.fullDesc }}</p>
              <div v-if="selectedProject.features" class="mt-6">
                <h4 class="text-white font-bold mb-2 text-xs uppercase tracking-widest">Ключевые особенности:</h4>
                <ul class="grid grid-cols-1 sm:grid-cols-2 gap-2 text-xs sm:text-sm text-gray-500">
                  <li v-for="feature in selectedProject.features" :key="feature" class="flex items-center gap-2">
                    <span class="h-1 w-1 rounded-full bg-sky-400"></span> {{ feature }}
                  </li>
                </ul>
              </div>
            </div>

            <div class="mt-10 flex gap-4">
              <a v-if="selectedProject.link && selectedProject.link !== '#'" :href="selectedProject.link" target="_blank" class="flex-1 text-center py-4 bg-white text-black font-bold rounded-xl hover:bg-sky-400 transition-all text-sm uppercase">Открыть проект</a>
              <a v-if="selectedProject.github && selectedProject.github !== '#'" :href="selectedProject.github" target="_blank" class="flex-1 text-center py-4 bg-[#1c1c1c] border border-[#2d2d2d] text-white font-bold rounded-xl hover:bg-[#222] transition-all text-sm uppercase">Исходный код</a>
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const selectedProject = ref(null);
const showFullList = ref(false);

const openProject = (project) => {
  selectedProject.value = project;
  document.body.style.overflow = 'hidden';
};

const closeModal = () => {
  selectedProject.value = null;
  document.body.style.overflow = '';
};

const visibleProjects = computed(() => {
  return showFullList.value ? projects : projects.slice(0, 3);
});

// Данные
const socials = [
  { 
    name: 'Email', 
    href: 'mailto:miryz@bk.ru',
    svg: '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect width="20" height="16" x="2" y="4" rx="2"/><path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/></svg>' 
  },
  { 
    name: 'GitHub', 
    href: 'https://github.com/Miryzzz', 
    svg: '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>' 
  },
  { 
    name: 'Telegram', 
    href: 'https://t.me/miryzik',
    svg: '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="22" y1="2" x2="11" y2="13"/><polyline points="22 2 15 22 11 13 2 9 22 2"/></svg>' 
  }
];

const stack = [
  { name: 'Vue.js 3', svg: '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"><path d="M24,1.45l-4,0L12,15.3L4,1.45L0,1.45L12,22.55L24,1.45z M16,1.45l-4,7L8,1.45L12,1.45z"/></svg>' },
  { name: 'Tailwind CSS', svg: '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"><path d="M12.001,4.8c-3.2,0-5.2,1.6-6,4.8c1.2-1.6,2.6-2.2,4.2-1.8c0.913,0.228,1.565,0.89,2.288,1.624C13.666,10.618,15.027,12,18.001,12c3.2,0,5.2-1.6,6-4.8c-1.2,1.6-2.6,2.2-4.2,1.8c-0.913-0.228-1.565-0.89-2.288-1.624C16.337,6.182,14.976,4.8,12.001,4.8z M6.001,12c-3.2,0-5.2,1.6-6,4.8c1.2-1.6,2.6-2.2,4.2-1.8c0.913,0.228,1.565,0.89,2.288,1.624c1.177,1.194,2.538,2.576,5.512,2.576c3.2,0,5.2-1.6,6-4.8c-1.2,1.6-2.6,2.2-4.2,1.8c-0.913-0.228-1.565-0.89-2.288-1.624C10.337,13.382,8.976,12,6.001,12z"/></svg>' },
  { name: 'Python', svg: '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"><path d="M14.25.18l.9.2.73.26.59.3.45.32.34.34.25.34.16.33.1.3.04.26.02.2l-.01.13V8.5h-2.1V6.4c0-.27-.13-.4-.38-.4h-4.14c-.27 0-.4.13-.4.4v2.1h2.1c.27 0 .4.13.4.4v4.14c0 .27-.13.4-.4.4h-2.1v2.1c0 .27.13.4.38.4h4.14c.27 0 .4-.13.4-.4v-2.1h2.1v3.9c0 .67-.22 1.23-.67 1.67-.44.44-1 .67-1.67.67H6.1c-.67 0-1.23-.23-1.67-.67-.44-.44-.67-1-.67-1.67V6.1c0-.67.23-1.23.67-1.67.44-.44 1-.67 1.67-.67h3.9c.67 0 1.23.23 1.67.67.44.44.67 1 .67 1.67V8.5h2.1V3.9c0-.67-.22-1.23-.67-1.67-.44-.44-1-.67-1.67-.67H10.1L9.1.18l-.9.2-.73.26-.59.3-.45.32-.34.34-.25.34-.16.33-.1.3-.04.26-.02.2.01.13v3.9H2.1V6.4c0-.27.13-.4.38-.4h4.14c.27 0 .4.13.4.4V8.5h-2.1c-.27 0-.4.13-.4.4v4.14c0 .27.13.4.4.4h2.1v2.1c0 .27-.13.4-.38.4H2.48c-.27 0-.4-.13-.4-.4V11.5h-2.1v3.9c0 .67.22 1.23.67 1.67.44.44 1 .67 1.67.67h11.8c.67 0 1.23-.23 1.67-.67.44-.44.67-1,.67-1.67V17.9h2.1v3.9c0 .67-.22 1.23-.67 1.67-.44.44-1 .67-1.67.67H6.1c-.67 0-1.23-.23-1.67-.67-.44-.44-.67-1-.67-1.67V2.1C3.76 1.43 3.99.87 4.43.43 4.87-.01 5.43-.24 6.1-.24h3.9L11.1.18l.9-.2.73-.26.59-.3.45-.32.34-.34.25-.34.16-.33.1-.3.04-.26.02-.2-.01-.13z"/></svg>' }
];

const projects = [
  { 
    title: 'Cyberpunk 2077 Promo', 
    desc: 'Адаптивная верстка игрового лендинга с эффектным дизайном.',
    fullDesc: 'Детальная верстка промо-сайта в стиле Cyberpunk 2077. Реализована характерная цветовая гамма, работа со сложными сетками изображений и полная адаптивность для мобильных устройств.',
    tags: ['Frontend', 'HTML/CSS', 'Адаптив', 'UI Design'],
    image: '/content/cyber.png', 
    link: '#', 
    features: ['Стилизованные UI-компоненты', 'Сложная сетка блоков', 'Игровой дизайн', 'Оптимизация изображений']
  },
  { 
    title: 'Apex Legends Tracker Bot', 
    desc: 'Telegram-бот для отслеживания игровой статистики и ротации карт.',
    fullDesc: 'Разработка Telegram-бота на Python (aiogram) для активных игроков Apex Legends. Бот парсит данные через API и в реальном времени сообщает о рангах пользователей и текущих картах в игре.',
    tags: ['Python', 'Aiogram', 'API', 'Scraping'],
    image: 'https://img.freepik.com/free-vector/telegram-concept-illustration_114360-1855.jpg',
    link: 'https://t.me/ApexLegendTracker_bot',
    github: 'https://github.com/MatveyTuzikov/ApexBot',
    features: ['Парсинг статистики (API)', 'Информация о ротации карт', 'Высокая скорость отклика', 'Поддержка команд']
  },
  { 
    title: 'ArtDomStroy', 
    desc: 'Корпоративный сайт для тюменского бизнеса по отделке фасадов.',
    fullDesc: 'Создание профессионального сайта для компании "АртДомСтрой". Основной фокус сделан на удобстве пользователя, демонстрации галереи выполненных работ и эффективном сборе заявок.',
    tags: ['Vue 3', 'Tailwind', 'Vite'],
    image: '/content/atrdomstroy.png',
    link: '#',
    features: ['Интерактивная галерея', 'Форма обратной связи', 'Высокая производительность', 'Vite-сборка']
  },
  { 
    title: 'NtfMarketPlace', 
    desc: 'Корпоративный сайт для тюменского бизнеса по отделке фасадов.',
    fullDesc: 'Создание профессионального сайта для компании "АртДомСтрой". Основной фокус сделан на удобстве пользователя, демонстрации галереи выполненных работ и эффективном сборе заявок.',
    tags: ['HTML5', 'CSS3',],
    image: '/content/nft.png',
    link: 'https://miryzzz.github.io/',
    features: ['Интерактивная галерея', 'Форма обратной связи', 'Высокая производительность', 'Vite-сборка']
  }
];
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>