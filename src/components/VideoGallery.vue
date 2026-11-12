<script setup>
import { ref } from 'vue'
import { Splide, SplideSlide } from '@splidejs/vue-splide'
import '@splidejs/vue-splide/css'

const videos = ref([
  { id: 1, image: '/1.png', title: 'Динамичный Reels для эксперта', duration: '0:45', url: 'https://www.youtube.com/playlist?list=PLZWeoMum6ly0' },
  { id: 2, image: '/2.png', title: 'Рекламный креатив для бренда', duration: '0:30', url: 'https://www.youtube.com/playlist?list=PLKIppp_Nqy-M' },
  { id: 3, image: '/3.png', title: 'Атмосферный монтаж мероприятия', duration: '1:15', url: 'https://www.youtube.com/playlist?list=PLW_5QEWfozlE' },
  { id: 4, image: '/5.png', title: 'YouTube Shorts с саунд-дизайном', duration: '0:58', url: 'https://www.youtube.com/playlist?list=PLf2BonFqcP_A' },
  { id: 5, image: '/4.png', title: 'Вертикальный ролик для соцсетей', duration: '0:40', url: 'https://www.youtube.com/playlist?list=PLOvAfrGh82gk' },
   
])

const splideOptions = {
  type: 'loop',
  perPage: 3,
  focus: 'center',      // Центральный слайд всегда получает класс .is-active
  gap: '1.5rem',
  pagination: true,
  arrows: true,         // На ПК стрелки включены
  breakpoints: {
    768: {
      perPage: 1,
      padding: '2.5rem',
      gap: '1rem',
      arrows: false     // На экранах меньше 768px (включая 400px) стрелки исчезают
    }
  }
}
</script>

<template>
  <section id="videos" class="py-20 max-w-5xl mx-auto px-5 border-t border-zinc-200 dark:border-zinc-800/80">
    <div class="text-center mb-12">
      <h2 class="text-3xl md:text-4xl font-bold text-zinc-900 dark:text-white mb-4">
        Видеомонтаж и Reels
      </h2>
      <p class="text-zinc-600 dark:text-zinc-400 max-w-xl mx-auto">
        Вертикальные ролики для соцсетей, цветокоррекция, динамичные склейки и работа со звуком.
      </p>
    </div>

    <!-- Добавили класс video-slider для стилизации центрального слайда -->
    <Splide :options="splideOptions" aria-label="Галерея видеомонтажа" class="video-slider">
      <SplideSlide v-for="video in videos" :key="video.id" class="py-4">
        <div class="slide-card aspect-9/16 rounded-2xl overflow-hidden relative group border border-zinc-200 dark:border-zinc-800 bg-zinc-900 transition-all duration-500">
          <img 
            :src="video.image" 
            :alt="video.title" 
            class="w-full h-full object-cover"
          />
          
          <span class="absolute top-3 right-3 text-xs font-mono font-semibold bg-black/70 text-white px-2.5 py-1 rounded-lg backdrop-blur-xs">
            {{ video.duration }}
          </span>

          <div class="absolute inset-0 bg-linear-to-t from-black/90 via-black/30 to-transparent flex flex-col justify-end p-5">
            <h3 class="text-white font-bold text-base mb-3 leading-snug">
              {{ video.title }}
            </h3>
            <a 
              :href="video.url" 
              target="_blank" 
              rel="noopener noreferrer"
              class="inline-flex items-center justify-center w-full py-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-semibold transition-colors"
            >
              ▶ Смотреть ролик
            </a>
          </div>
        </div>
      </SplideSlide>
    </Splide>
  </section>
</template>

<style scoped>
/* Боковые слайды слегка уменьшаем и приглушаем */
.video-slider :deep(.splide__slide) .slide-card {
  transform: scale(0.9);
  opacity: 0.55;
}

/* Центральный активный слайд увеличиваем и делаем ярким */
.video-slider :deep(.splide__slide.is-active) .slide-card {
  transform: scale(1.04);
  opacity: 1;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.3);
  border-color: rgb(99 102 241 / 0.6); /* Подсветка рамки цветом indigo-500 */
}
</style>
 