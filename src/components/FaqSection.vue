<script setup>
import { ref } from 'vue'

const activeIndex = ref(0)

const faqs = ref([
  {
    question: 'Сколько времени занимает создание сайта под ключ?',
    answer: 'Простой лендинг с адаптивной вёрсткой занимает от 3 до 5 дней. Многостраничное приложение или каталог с фильтрацией на Vue 3 — от 7 до 14 дней в зависимости от объёма контента.'
  },
  {
    question: 'В каком формате присылать исходники для видеомонтажа?',
    answer: 'Подойдут любые исходники в хорошем качестве (ссылкой на Яндекс.Диск, Google Drive или Telegram). Желательно заранее описать задачу, референсы и нужный формат (вертикальный 9:16 для Reels/Shorts или горизонтальный 16:9).'
  },
  {
    question: 'Помогаете ли вы с покупкой домена и загрузкой сайта в сеть?',
    answer: 'Да, после утверждения проекта я помогаю зарегистрировать домен, настроить бесплатный SSL-сертификат и выгрузить готовый сайт на быстрый хостинг.'
  },
  {
    question: 'Можно ли внести правки в процессе работы?',
    answer: 'Конечно. Мы разбиваем работу на этапы: сначала согласовываем структуру и черновой монтаж или прототип сайта, и на каждом шаге вы можете вносить корректировки.'
  }
])

const toggleItem = (index) => {
  activeIndex.value = activeIndex.value === index ? null : index
}
</script>

<template>
  <section id="faq" class="py-20 max-w-3xl mx-auto px-5 border-t border-zinc-200 dark:border-zinc-800/80">
    <div class="text-center mb-12">
      <h2 class="text-3xl md:text-4xl font-bold text-zinc-900 dark:text-white mb-4">
        Частые вопросы
      </h2>
      <p class="text-zinc-600 dark:text-zinc-400">
        Ответы на популярные вопросы о сроках, исходниках и процессе работы.
      </p>
    </div>

    <div class="space-y-3">
      <div 
        v-for="(item, index) in faqs" 
        :key="index"
        class="rounded-2xl border border-zinc-200 dark:border-zinc-800 bg-white dark:bg-zinc-900 overflow-hidden transition-colors"
      >
        <button 
          @click="toggleItem(index)"
          class="w-full px-6 py-4 text-left flex items-center justify-between gap-4 font-semibold text-zinc-900 dark:text-zinc-100 hover:text-indigo-600 dark:hover:text-indigo-400 transition-colors cursor-pointer"
        >
          <span>{{ item.question }}</span>
          <span 
            :class="activeIndex === index ? 'rotate-45 text-indigo-600 dark:text-indigo-400' : 'text-zinc-400'"
            class="text-2xl leading-none transition-transform duration-300 select-none shrink-0"
          >
            +
          </span>
        </button>

        <!-- Плавный контейнер через CSS Grid -->
        <div 
          :class="activeIndex === index ? 'grid-rows-[1fr] opacity-100' : 'grid-rows-[0fr] opacity-0'"
          class="grid transition-all duration-300 ease-out"
        >
          <div class="overflow-hidden">
            <div class="px-6 pb-5 pt-3 text-sm text-zinc-600 dark:text-zinc-400 leading-relaxed border-t border-zinc-100 dark:border-zinc-800/60">
              {{ item.answer }}
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>
