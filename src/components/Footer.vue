<template>
  <footer class="footer">

    <!-- Карта -->
    <div class="footer_map">
      <div id="yandex-map" style="width: 100%; height: 100%;"></div>
    </div>

    <!-- Основная часть футера -->
    <div class="footer_container">

      <div class="footer_left">
        <div class="footer_logo">
          <img
              :src="logo"
              :srcset="logo + ' 1x, ' + logo2x + ' 2x'"
              alt="BLOOM BOOM"
              class="header_logo_img"
          />
        </div>

        <div class="footer_brand">
          <a href="/" aria-label="На главную" class="brand_name">BLOOM BOOM</a>

          <div class="brand_description">
            Оптовая и розничная торговля<br>
            стабилизированными цветами
          </div>
        </div>
      </div>

      <div class="footer_right">
        <div class="work_time">Время работы: ежедневно с 10:00 до 18:00</div>
        <a href="tel:+70000000000" class="phone">+7 000 000 00 00</a>
      </div>

    </div>

    <!-- Низ футера -->
    <div class="footer_bottom">
      © 2025 BLOOM BOOM. Все права защищены.
    </div>

  </footer>
</template>

<script setup>
import { onMounted } from "vue"

// импорт логотипов
import logo from '../assets/img/logo.png'
import logo2x from '../assets/img/logo@2x.png'


// Функция инициализации Яндекс-карты
const initMap = () => {
  if (typeof ymaps === "undefined") {
    console.warn("Yandex Maps API не загружен")
    return
  }

  ymaps.ready(() => {
    const center = [55.76, 37.64] // Можешь поменять на нужные координаты

    const map = new ymaps.Map("yandex-map", {
      center,
      zoom: 12,
      controls: ["zoomControl"],
    })

    const placemark = new ymaps.Placemark(
        center,
        {
          hintContent: "BLOOM BOOM",
          balloonContent: "<strong>BLOOM BOOM</strong><br>Телефон: +7 000 000 00 00",
        },
        {
          preset: "islands#redIcon",
        }
    )

    map.geoObjects.add(placemark)

    map.behaviors.disable("scrollZoom")
  })
}

onMounted(() => {
  // Если карта не подключена через index.html — загружаем скрипт динамически
  if (typeof ymaps === "undefined") {
    const script = document.createElement("script")
    script.src = "https://api-maps.yandex.ru/2.1/?lang=ru_RU"
    script.onload = initMap
    document.head.appendChild(script)
  } else {
    initMap()
  }
})
</script>
