<script setup>
import { ref, computed } from 'vue'

const currentFilter = ref('all')

// Заглушки проектов (потом заменишь на свои реальные ссылки и скриншоты)
const projects = ref([
  {
    id: 1,
    title: 'Корпоративный сайт студии',
    category: 'landing',
    categoryLabel: 'Лендинг',
    description: 'Адаптивная вёрстка с анимациями, формой заявки и высокой скоростью загрузки.',
    tech: ['Vue 3', 'Tailwind v4', 'Vite'],
    url: '#'
  },
  {
    id: 2,
    title: 'Интернет-магазин аксессуаров',
    category: 'spa',
    categoryLabel: 'Веб-приложение',
    description: 'Каталог товаров с фильтрацией, корзиной на LocalStorage и тёмной темой.',
    tech: ['Vue 3', 'VueUse', 'Pinia'],
    url: '#'
  },
  {
    id: 3,
    title: 'Промо-страница курса',
    category: 'landing',
    categoryLabel: 'Лендинг',
    description: 'Продающая посадочная страница с интерактивным калькулятором и таймером.',
    tech: ['HTML5', 'Tailwind CSS', 'JS'],
    url: '#'
  },
  {
    id: 4,
    title: 'Дашборд аналитики',
    category: 'spa',
    categoryLabel: 'Веб-приложение',
    description: 'Личный кабинет пользователя с загрузкой данных по API и графиками.',
    tech: ['Vue 3', 'REST API', 'Tailwind'],
    url: '#'
  }
])

const filteredProjects = computed(() => {
  if (currentFilter.value === 'all') return projects.value
  return projects.value.filter(project => project.category === currentFilter.value)
})
</script>

<template>
  <section id="projects" class="py-20 max-w-5xl mx-auto px-5 border-t border-zinc-200 dark:border-zinc-800/80">
    <div class="text-center mb-12">
      <h2 class="text-3xl md:text-4xl font-bold text-zinc-900 dark:text-white mb-4">
        Разработка сайтов
      </h2>
      <p class="text-zinc-600 dark:text-zinc-400 max-w-xl mx-auto">
        Примеры вёрстки и одностраничных приложений, собранных с упором на чистый код и адаптивность.
      </p>
    </div>

    <!-- Кнопки фильтрации -->
    <div class="flex flex-wrap justify-center gap-2 mb-10">
      <button 
        @click="currentFilter = 'all'"
        :class="currentFilter === 'all' ? 'bg-indigo-600 text-white shadow-md shadow-indigo-600/20' : 'bg-zinc-200/70 dark:bg-zinc-800 text-zinc-700 dark:text-zinc-300 hover:bg-zinc-300 dark:hover:bg-zinc-700'"
        class="px-5 py-2 rounded-xl text-sm font-semibold transition-all cursor-pointer"
      >
        Все работы
      </button>
      <button 
        @click="currentFilter = 'landing'"
        :class="currentFilter === 'landing' ? 'bg-indigo-600 text-white shadow-md shadow-indigo-600/20' : 'bg-zinc-200/70 dark:bg-zinc-800 text-zinc-700 dark:text-zinc-300 hover:bg-zinc-300 dark:hover:bg-zinc-700'"
        class="px-5 py-2 rounded-xl text-sm font-semibold transition-all cursor-pointer"
      >
        Лендинги
      </button>
      <button 
        @click="currentFilter = 'spa'"
        :class="currentFilter === 'spa' ? 'bg-indigo-600 text-white shadow-md shadow-indigo-600/20' : 'bg-zinc-200/70 dark:bg-zinc-800 text-zinc-700 dark:text-zinc-300 hover:bg-zinc-300 dark:hover:bg-zinc-700'"
        class="px-5 py-2 rounded-xl text-sm font-semibold transition-all cursor-pointer"
      >
        Веб-приложения
      </button>
    </div>

    <!-- Сетка проектов -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <article 
        v-for="project in filteredProjects" 
        :key="project.id"
        class="group p-6 rounded-2xl bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800 hover:border-indigo-500/50 transition-all flex flex-col justify-between shadow-xs"
      >
        <div>
          <div class="flex items-center justify-between gap-2 mb-3">
            <span class="text-xs font-semibold px-3 py-1 rounded-lg bg-indigo-50 dark:bg-indigo-950/60 text-indigo-600 dark:text-indigo-400">
              {{ project.categoryLabel }}
            </span>
            <a 
              :href="project.url" 
              target="_blank" 
              rel="noopener noreferrer"
              class="text-sm font-medium text-zinc-500 hover:text-indigo-600 dark:hover:text-indigo-400 transition-colors"
            >
              Открыть ↗
            </a>
          </div>

          <h3 class="text-xl font-bold text-zinc-900 dark:text-white mb-2 group-hover:text-indigo-600 dark:group-hover:text-indigo-400 transition-colors">
            {{ project.title }}
          </h3>
          <p class="text-sm text-zinc-600 dark:text-zinc-400 leading-relaxed mb-6">
            {{ project.description }}
          </p>
        </div>

        <!-- Теги технологий -->
        <div class="flex flex-wrap gap-2 pt-4 border-t border-zinc-100 dark:border-zinc-800/80">
          <span 
            v-for="tag in project.tech" 
            :key="tag"
            class="text-xs font-mono text-zinc-500 dark:text-zinc-400 bg-zinc-100 dark:bg-zinc-800/80 px-2.5 py-1 rounded-md"
          >
            {{ tag }}
          </span>
        </div>
      </article>
    </div>
  </section>
</template>
