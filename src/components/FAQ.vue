<template>
  <section class="faq">
    <div class="faq_container">
      <h2 class="faq_title">Частые вопросы</h2>

      <div class="faq_list">
        <div
            class="faq_item"
            v-for="(item, index) in faqList"
            :key="index"
            :class="{ active: activeIndex === index }"
        >
          <button
              class="faq_question"
              @click="toggle(index)"
              @keydown.enter.prevent="toggle(index)"
              @keydown.space.prevent="toggle(index)"
          >
            <span>{{ item.question }}</span>

            <!-- Иконка -->
            <svg class="faq_icon" width="20" height="20" viewBox="0 0 20 20" fill="none">
              <path
                  d="M5 7.5L10 12.5L15 7.5"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
              />
            </svg>
          </button>

          <!-- Ответ -->
          <div v-show="activeIndex === index" class="faq_answer">
            <p v-html="item.answer"></p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue"

const activeIndex = ref(null)

const faqList = [
  {
    question: "Что такое франшиза?",
    answer:
        "Франшиза — это бизнес-модель, при которой владелец бренда (франчайзер) передает право на использование своей торговой марки, бизнес-процессов и ноу-хау другому лицу (франчайзи) за определенное вознаграждение.",
  },
  {
    question: "Из чего состоит франшиза?",
    answer:
        "Франшиза обычно включает в себя: брендбук, бизнес-план, маркетинговые материалы, обучение персонала, стандарты качества, поставщиков и постоянную поддержку от франчайзера.",
  },
  {
    question: "Сколько стоит франшиза?",
    answer:
        "Стоимость франшизы зависит от многих факторов: известности бренда, региона, размера бизнеса. Обычно включает паушальный взнос (разовый платеж) и роялти (ежемесячные отчисления).",
  },
  {
    question: "На что обратить внимание при выборе франшизы?",
    answer:
        "При выборе франшизы важно учитывать: репутацию франчайзера, отзывы других франчайзи, прозрачность условий, размер инвестиций, срок окупаемости, уровень поддержки и перспективы развития бренда.",
  },
]

// логика аккордеона
const toggle = i => {
  activeIndex.value = activeIndex.value === i ? null : i
}
</script>
