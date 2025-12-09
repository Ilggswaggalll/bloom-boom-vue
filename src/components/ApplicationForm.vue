<template>
  <section class="application_section">
    <h2 class="application_title">
      Оставьте заявку и получите<br />
      индивидуальный расчет стоимости
    </h2>

    <form class="application_container" @submit.prevent="submitForm">
      <label>
        <input
            type="text"
            placeholder="Ваше имя"
            class="application_form-input"
            v-model="name"
            required
        />
      </label>

      <label>
        <input
            type="tel"
            placeholder="Ваш телефон"
            class="application_form-input"
            v-model="phone"
            required
        />
      </label>

      <button type="submit" class="application_form-button">
        Получить индивидуальный расчет стоимости
      </button>
    </form>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// реактивные поля
const name = ref('')
const phone = ref('')

// отправка формы
const submitForm = () => {
  console.log("Имя:", name.value)
  console.log("Телефон:", phone.value)

  // здесь можно сделать реальную отправку запроса (пример)
  /*
  await fetch('/api/send', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name: name.value, phone: phone.value })
  })
  */

  alert("Заявка отправлена!")

  // сброс формы
  name.value = ''
  phone.value = ''
}
</script>
