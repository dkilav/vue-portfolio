<script setup>
import { ref } from 'vue'
import { useClipboard } from '@vueuse/core'

const myEmail = 'vlad5222vd@gmail.com'
const { copy, copied } = useClipboard()

const form = ref({
  name: '',
  contact: '',
  service: 'Создание сайта',
  message: ''
})

const submitForm = () => {
  if (!form.value.name.trim()) return

  const subject = `Заявка с сайта Wladder: ${form.value.service}`
  const body = `Имя: ${form.value.name}\nКонтакт для связи: ${form.value.contact}\nУслуга: ${form.value.service}\n\nЗадача:\n${form.value.message || 'Не указана'}`
  
  // Открываем почтовый клиент с уже заполненным письмом на твой адрес
  window.location.href = `mailto:${myEmail}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`

  form.value = { name: '', contact: '', service: 'Создание сайта', message: '' }
}
</script>

<template>
  <footer id="contacts" class="pt-20 pb-10 border-t border-zinc-200 dark:border-zinc-800/80 bg-zinc-100/50 dark:bg-zinc-900/40">
    <div class="max-w-5xl mx-auto px-5">
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-12 mb-16">
        
        <!-- Левая колонка: Прямые контакты -->
        <div>
          <h2 class="text-3xl md:text-4xl font-bold text-zinc-900 dark:text-white mb-4">
            Обсудим ваш проект?
          </h2>
          <p class="text-zinc-600 dark:text-zinc-400 mb-8 leading-relaxed">
            Напишите мне на электронную почту или оставьте заявку в форме. Отвечу в течение пары часов, подскажу по срокам и стоимости.
          </p>

          <div class="space-y-4">
            <!-- Прямая кнопка открытия почты -->
            <a 
              :href="`mailto:${myEmail}`"
              class="flex items-center justify-between p-4 rounded-2xl bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800 hover:border-indigo-500 transition-colors group"
            >
              <div>
                <span class="block text-xs text-zinc-500">Быстрая связь</span>
                <span class="font-semibold text-zinc-900 dark:text-white group-hover:text-indigo-600 dark:group-hover:text-indigo-400 transition-colors">
                  Написать письмо на Email
                </span>
              </div>
              <span class="text-indigo-600 dark:text-indigo-400 font-bold">→</span>
            </a>

            <!-- Копирование почты в один клик -->
            <div class="flex items-center justify-between p-4 rounded-2xl bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800">
              <div>
                <span class="block text-xs text-zinc-500">Электронная почта</span>
                <span class="font-mono text-sm font-semibold text-zinc-900 dark:text-white">
                  {{ myEmail }}
                </span>
              </div>
              <button 
                @click="copy(myEmail)"
                class="px-3.5 py-2 rounded-xl text-xs font-semibold bg-indigo-50 dark:bg-indigo-950 text-indigo-600 dark:text-indigo-400 hover:bg-indigo-100 dark:hover:bg-indigo-900 transition-colors cursor-pointer"
              >
                {{ copied ? 'Скопировано! ✓' : 'Копировать' }}
              </button>
            </div>
          </div>
        </div>

        <!-- Правая колонка: Форма заявки -->
        <form @submit.prevent="submitForm" class="p-6 md:p-8 rounded-2xl bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800 space-y-4 shadow-xs">
          <div>
            <label class="block text-xs font-semibold uppercase tracking-wider text-zinc-500 mb-1.5">Ваше имя</label>
            <input 
              v-model="form.name"
              type="text" 
              required
              placeholder="Александр"
              class="w-full px-4 py-2.5 rounded-xl border border-zinc-300 dark:border-zinc-700 bg-zinc-50 dark:bg-zinc-950 text-zinc-900 dark:text-white focus:outline-none focus:ring-2 focus:ring-indigo-500"
            />
          </div>

          <div>
            <label class="block text-xs font-semibold uppercase tracking-wider text-zinc-500 mb-1.5">Почта или телефон</label>
            <input 
              v-model="form.contact"
              type="text" 
              required
              placeholder="name@mail.com или +373..."
              class="w-full px-4 py-2.5 rounded-xl border border-zinc-300 dark:border-zinc-700 bg-zinc-50 dark:bg-zinc-950 text-zinc-900 dark:text-white focus:outline-none focus:ring-2 focus:ring-indigo-500"
            />
          </div>

          <div>
            <label class="block text-xs font-semibold uppercase tracking-wider text-zinc-500 mb-1.5">Интересующая услуга</label>
            <select 
              v-model="form.service"
              class="w-full px-4 py-2.5 rounded-xl border border-zinc-300 dark:border-zinc-700 bg-zinc-50 dark:bg-zinc-950 text-zinc-900 dark:text-white focus:outline-none focus:ring-2 focus:ring-indigo-500"
            >
              <option value="Создание сайта">Создание сайта с нуля</option>
              <option value="Видеомонтаж">Видеомонтаж / Reels</option>
              <option value="Комплекс">Сайт + Видеоконтент</option>
            </select>
          </div>

          <div>
            <label class="block text-xs font-semibold uppercase tracking-wider text-zinc-500 mb-1.5">Кратко о задаче</label>
            <textarea 
              v-model="form.message"
              rows="3" 
              placeholder="Опишите идею или прикрепите ссылку на референс..."
              class="w-full px-4 py-2.5 rounded-xl border border-zinc-300 dark:border-zinc-700 bg-zinc-50 dark:bg-zinc-950 text-zinc-900 dark:text-white focus:outline-none focus:ring-2 focus:ring-indigo-500"
            ></textarea>
          </div>

          <button 
            type="submit"
            class="w-full py-3 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-semibold shadow-md shadow-indigo-600/20 transition-all cursor-pointer"
          >
            Отправить заявку на Email
          </button>
        </form>

      </div>

      <!-- Нижняя строка копирайта -->
      <div class="pt-8 border-t border-zinc-200 dark:border-zinc-800 flex flex-col sm:flex-row items-center justify-between gap-4 text-sm text-zinc-500">
        <span class="font-logo text-2xl text-indigo-600 dark:text-indigo-400">Wladder</span>
        <span>© {{ new Date().getFullYear() }} Все права защищены. Сделано на Vue 3 & Tailwind.</span>
      </div>

    </div>
  </footer>
</template>
