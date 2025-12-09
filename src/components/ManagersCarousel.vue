<template>
  <section class="individual_manager">
    <h2 class="individual_manager_title">
      Для открытия франшизы за вами закрепляется индивидуальный менеджер
    </h2>

    <p class="individual_manager_description">
      Познакомтесь со своими будущими партнерами, которые за руку доведут вас до<br>
      магазина c оборотом в 2 000 000 рублей в месяц
    </p>

    <div class="individual_manager_container">
      <!-- Кнопка назад -->
      <button
          class="nav-btn prev"
          :disabled="currentIndex === 0"
          @click="prev"
      >
        ‹
      </button>

      <!-- Обертка для скролла -->
      <div class="individual_manager_wrapper" ref="wrapper">
        <div
            class="individual_manager_item"
            v-for="(manager, index) in managers"
            :key="index"
        >
          <div class="manager_photo">
            <img
                :src="manager.img"
                :srcset="manager.srcset"
                :alt="manager.alt"
                loading="lazy"
            />
          </div>

          <p class="manager_description">{{ manager.role }}</p>
          <p class="manager_description">{{ manager.experience }}</p>
          <button class="manager_button">Задать вопрос {{ manager.name }}</button>
        </div>
      </div>

      <!-- Кнопка вперед -->
      <button
          class="nav-btn next"
          :disabled="currentIndex >= maxIndex"
          @click="next"
      >
        ›
      </button>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from 'vue'

// Импорты изображений (замени пути, если у тебя другая структура)
// Положи картинки в src/assets/img/
import Ilgiz from '../assets/img/Ilgiz.jpg'
import Ilgiz2x from '../assets/img/Ilgiz@2x.jpg'

import Andrei from '../assets/img/Andrei.jpg'
import Andrei2x from '../assets/img/Andrei@2x.jpg'

import Nikita from '../assets/img/Nikita.jpg'
import Nikita2x from '../assets/img/Nikita@2x.jpg'

import Artem from '../assets/img/Artem.jpg'
import Artem2x from '../assets/img/Artem@2x.jpg'

import German from '../assets/img/German.jpg'
import German2x from '../assets/img/German@2x.jpg'

// Массив менеджеров
const managers = [
  {
    name: "Ильгиз",
    img: Ilgiz,
    srcset: `${Ilgiz} 1x, ${Ilgiz2x} 2x`,
    alt: "Фотография менеджера Ильгиза",
    role: "Фронтенд-разработчик",
    experience: "Опыт отсутствует"
  },
  {
    name: "Андрей",
    img: Andrei,
    srcset: `${Andrei} 1x, ${Andrei2x} 2x`,
    alt: "Фотография менеджера Андрея",
    role: "Бэкенд-разработчик",
    experience: "Опыт присутствует"
  },
  {
    name: "Никита",
    img: Nikita,
    srcset: `${Nikita} 1x, ${Nikita2x} 2x`,
    alt: "Фотография менеджера Никиты",
    role: "Бэкенд-разработчик",
    experience: "Опыт присутствует"
  },
  {
    name: "Артем",
    img: Artem,
    srcset: `${Artem} 1x, ${Artem2x} 2x`,
    alt: "Фотография менеджера Артема",
    role: "Тимлид",
    experience: "Опыт отсутствует"
  },
  {
    name: "Герман",
    img: German,
    srcset: `${German} 1x, ${German2x} 2x`,
    alt: "Фотография менеджера Германа",
    role: "Ищет квартиру",
    experience: "Опыт отсутствует"
  }
]

const wrapper = ref(null)
const currentIndex = ref(0)
const visibleCount = ref(3)
const itemsCount = managers.length

// Расчёт количества карточек на экране
const updateVisibleCount = () => {
  const w = window.innerWidth
  if (w <= 768) visibleCount.value = 1
  else if (w <= 1024) visibleCount.value = 2
  else visibleCount.value = 3
}

// Максимальный индекс прокрутки
const maxIndex = computed(() => Math.max(0, itemsCount - visibleCount.value))

// Скролл к элементу
const scrollToCurrent = () => {
  const wrapperEl = wrapper.value
  if (!wrapperEl) return

  const item = wrapperEl.children[currentIndex.value]
  if (!item) return

  const scrollPosition = item.offsetLeft - wrapperEl.offsetLeft

  wrapperEl.scrollTo({
    left: scrollPosition,
    behavior: 'smooth'
  })
}

// Кнопки
const prev = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--
    scrollToCurrent()
  }
}

const next = () => {
  if (currentIndex.value < maxIndex.value) {
    currentIndex.value++
    scrollToCurrent()
  }
}

let resizeHandler = () => {
  updateVisibleCount()
  if (currentIndex.value > maxIndex.value) {
    currentIndex.value = maxIndex.value
  }
}

onMounted(() => {
  updateVisibleCount()
  window.addEventListener('resize', resizeHandler)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeHandler)
})
</script>
