<template>
  <section class="advantages_of_stabilized_flowers">
    <h2 class="advantages_title">
      6 несравненных плюсов стабилизированных цветов
    </h2>

    <div class="advantages_container">
      <div
          class="advantages_item"
          v-for="(advantage, index) in advantages"
          :key="index"
      >
        <div class="advantages_icon"></div>
        <p class="advantages_advantage">{{ advantage }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
const advantages = [
  "Сохраняют аромат только что сорванных цветов",
  "Не требуют специализированного ухода",
  "Абсолютно безвредны для домашних животных",
  "Мягкие и пластичные, совсем как живые цветы",
  "Гипоаллергенны",
  "Внешний вид, который держится годами",
]
</script>
