<script setup>
import { ref } from 'vue'
import { useDark, useToggle } from '@vueuse/core'

// Умная тёмная тема из VueUse (сама запоминает выбор в браузере)
const isDark = useDark()
const toggleDark = useToggle(isDark)

const isMenuOpen = ref(false)
</script>

<template>
  <header class="sticky top-0 z-50 backdrop-blur-md bg-zinc-50/80 dark:bg-zinc-950/80 border-b border-zinc-200 dark:border-zinc-800/80">
    <nav class="max-w-5xl mx-auto px-5 h-16 flex items-center justify-between">
      
      <!-- Фирменный логотип Wladder шрифтом My Soul -->
      <a href="#" class="font-logo text-3xl md:text-4xl text-indigo-600 dark:text-indigo-400 tracking-wide select-none">
        Wladder
      </a>

      <!-- Меню для ПК -->
      <ul class="hidden md:flex items-center gap-8 text-sm font-medium text-zinc-600 dark:text-zinc-300">
        <li><a href="#projects" class="hover:text-indigo-600 dark:hover:text-indigo-400 transition-colors">Сайты</a></li>
        <li><a href="#videos" class="hover:text-indigo-600 dark:hover:text-indigo-400 transition-colors">Видеомонтаж</a></li>
        <li><a href="#faq" class="hover:text-indigo-600 dark:hover:text-indigo-400 transition-colors">Вопросы</a></li>
        <li><a href="#contacts" class="hover:text-indigo-600 dark:hover:text-indigo-400 transition-colors">Контакты</a></li>
      </ul>

      <!-- Кнопки справа: Тема и Мобильное меню -->
      <div class="flex items-center gap-3">
        <button 
          @click="toggleDark()" 
          aria-label="Переключить тему"
          class="p-2 rounded-xl bg-zinc-200/70 dark:bg-zinc-800 text-zinc-700 dark:text-zinc-200 hover:bg-zinc-300 dark:hover:bg-zinc-700 transition-colors cursor-pointer"
        >
          <span v-if="isDark">☀️</span>
          <span v-else>🌙</span>
        </button>

        <button 
          @click="isMenuOpen = !isMenuOpen" 
          class="md:hidden p-2 rounded-xl bg-zinc-200/70 dark:bg-zinc-800 text-zinc-700 dark:text-zinc-200 cursor-pointer"
        >
          {{ isMenuOpen ? '✕' : '☰' }}
        </button>
      </div>
    </nav>

    <!-- Выпадающее меню для мобильных телефонов -->
    <div v-if="isMenuOpen" class="md:hidden border-b border-zinc-200 dark:border-zinc-800 bg-zinc-50 dark:bg-zinc-950 px-5 py-4 space-y-3">
      <a @click="isMenuOpen = false" href="#projects" class="block text-base font-medium py-1">Сайты</a>
      <a @click="isMenuOpen = false" href="#videos" class="block text-base font-medium py-1">Видеомонтаж</a>
      <a @click="isMenuOpen = false" href="#faq" class="block text-base font-medium py-1">Вопросы</a>
      <a @click="isMenuOpen = false" href="#contacts" class="block text-base font-medium py-1">Контакты</a>
    </div>
  </header>
</template>
