<template>
  <section class="consultation_section">
    <h2 class="consultation_title">
      Остались вопросы?
    </h2>

    <p class="consultation_text">
      Задайте их прямо сейчас и получите консультацию в течение 15 минут
    </p>

    <form class="consultation_container" @submit.prevent="submitForm">

      <!-- Текстовое сообщение -->
      <label>
        <textarea
            class="consultation_question-input"
            placeholder="Ваше сообщение..."
            v-model="message"
            ref="textarea"
            @input="autoResize"
        ></textarea>
      </label>

      <div class="consultation_bottom-row">
        <!-- Телефон -->
        <label>
          <input
              type="tel"
              class="consultation_form-input"
              placeholder="+7 (000) 000-00-00"
              v-model="phone"
              required
          />
        </label>

        <!-- Кнопка -->
        <button type="submit" class="consultation_form-button">
          Получить консультацию
        </button>
      </div>

    </form>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue"

const message = ref("")
const phone = ref("")
const textarea = ref(null)

// авто-увеличение textarea
const autoResize = () => {
  const el = textarea.value
  if (!el) return
  el.style.height = "auto"
  el.style.height = el.scrollHeight + "px"
}

onMounted(() => {
  autoResize()
})

// отправка формы
const submitForm = () => {
  console.log("Сообщение:", message.value)
  console.log("Телефон:", phone.value)

  alert("Заявка отправлена!")

  // сброс значений
  message.value = ""
  phone.value = ""

  // сброс высоты textarea
  setTimeout(() => autoResize(), 0)
}
</script>
