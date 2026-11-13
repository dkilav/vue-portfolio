<script setup>
import { ref, computed } from 'vue'

const currentFilter = ref('all')

const services = ref([
  {
    id: 1,
    title: 'Продающий лендинг под ключ',
    category: 'landing',
    categoryLabel: 'Лендинг',
    description: 'Одностраничный сайт для товара, услуги или мероприятия с адаптацией под телефоны, высокой скоростью загрузки и формой заявки.',
    tech: ['Vue 3', 'Tailwind CSS', 'Адаптивность']
  },
  {
    id: 2,
    title: 'Интерактивное веб-приложение',
    category: 'spa',
    categoryLabel: 'Веб-приложение',
    description: 'Современный сайт с динамической фильтрацией, калькулятором стоимости, тёмной темой и плавными анимациями без перезагрузки страниц.',
    tech: ['Vue 3', 'JavaScript', 'Vite']
  },
  {
    id: 3,
    title: 'Сайт-визитка или портфолио',
    category: 'landing',
    categoryLabel: 'Лендинг',
    description: 'Упаковка личного бренда специалиста или небольшой студии: галерея работ, ответы на частые вопросы и быстрая связь с клиентом.',
    tech: ['HTML5', 'Tailwind CSS', 'SEO-база']
  },
  {
    id: 4,
    title: 'Адаптивная вёрстка по макету',
    category: 'spa',
    categoryLabel: 'Веб-приложение',
    description: 'Аккуратный перенос вашего дизайна из Figma в чистый, современный код с корректным отображением на любых мониторах и смартфонах.',
    tech: ['Figma', 'Tailwind CSS', 'Чистый код']
  }
])

const filteredServices = computed(() => {
  if (currentFilter.value === 'all') return services.value
  return services.value.filter(item => item.category === currentFilter.value)
})
</script>

<template>
  <section id="projects" class="py-20 max-w-5xl mx-auto px-5 border-t border-zinc-200 dark:border-zinc-800/80">
    <div class="text-center mb-12">
      <h2 class="text-3xl md:text-4xl font-bold text-zinc-900 dark:text-white mb-4">
        Разработка сайтов
      </h2>
      <p class="text-zinc-600 dark:text-zinc-400 max-w-xl mx-auto">
        Форматы сайтов и веб-интерфейсов, которые я создаю с упором на чистый код, скорость работы и удобство на телефонах.
      </p>
    </div>

    <!-- Кнопки фильтрации -->
    <div class="flex flex-wrap justify-center gap-2 mb-10">
      <button 
        @click="currentFilter = 'all'"
        :class="currentFilter === 'all' ? 'bg-indigo-600 text-white shadow-md shadow-indigo-600/20' : 'bg-zinc-200/70 dark:bg-zinc-800 text-zinc-700 dark:text-zinc-300 hover:bg-zinc-300 dark:hover:bg-zinc-700'"
        class="px-5 py-2 rounded-xl text-sm font-semibold transition-all cursor-pointer"
      >
        Все форматы
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

    <!-- Сетка услуг -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <article 
        v-for="service in filteredServices" 
        :key="service.id"
        class="group p-6 rounded-2xl bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800 hover:border-indigo-500/50 transition-all flex flex-col justify-between shadow-xs"
      >
        <div>
          <div class="flex items-center justify-between gap-2 mb-3">
            <span class="text-xs font-semibold px-3 py-1 rounded-lg bg-indigo-50 dark:bg-indigo-950/60 text-indigo-600 dark:text-indigo-400">
              {{ service.categoryLabel }}
            </span>
            <a 
              href="#contacts" 
              class="text-sm font-medium text-zinc-500 hover:text-indigo-600 dark:hover:text-indigo-400 transition-colors"
            >
              Заказать ↓
            </a>
          </div>

          <h3 class="text-xl font-bold text-zinc-900 dark:text-white mb-2 group-hover:text-indigo-600 dark:group-hover:text-indigo-400 transition-colors">
            {{ service.title }}
          </h3>
          <p class="text-sm text-zinc-600 dark:text-zinc-400 leading-relaxed mb-6">
            {{ service.description }}
          </p>
        </div>

        <!-- Теги технологий -->
        <div class="flex flex-wrap gap-2 pt-4 border-t border-zinc-100 dark:border-zinc-800/80">
          <span 
            v-for="tag in service.tech" 
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
