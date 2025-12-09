<!-- src/components/Header.vue -->
<template>
  <header class="header">
    <div class="header_container">
      <div class="header_left">
        <div class="header_logo">
          <img :src="logo" alt="BLOOM BOOM" class="header_logo_img" />
        </div>
        <div class="header_brand">
          <a href="/" aria-label="На главную" class="brand_name">BLOOM BOOM</a>
          <div class="brand_description">
            Оптовая и розничная торговля<br/>стабилизированными цветами
          </div>
        </div>
      </div>
      <div class="header_right">
        <div class="work_time">Время работы: ежедневно с 10:00 до 18:00</div>
        <a href="tel:+70000000000" class="phone">+7 000 000 00 00</a>
        <button class="callback_btn">Заказать обратный звонок</button>
      </div>
    </div>
  </header>
</template>

<script setup>
import logo from '../assets/img/logo.png'
</script>
