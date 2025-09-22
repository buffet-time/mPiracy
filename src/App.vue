<script setup lang="ts">
import { onMounted, ref } from 'vue'
import gif from '/gif.gif'

const startingTime = new Date()
const tempMinute = startingTime.getMinutes()
const minute = `${tempMinute < 10 ? '0' : ''}${tempMinute}`
const hour = startingTime.getHours()
const day = startingTime.getDate()
const month = startingTime.getMonth()
const year = startingTime.getFullYear()

const hoursAndMinutes = ref(`${hour + 1}h${minute}`)
const date = ref(`${day}.${month}.${year}`)
const timerText = ref('')

function startTimer(duration: number) {
  let timer = duration,
    minutes,
    seconds

  function countdown() {
    minutes = parseInt(String(timer / 60), 10)
    seconds = parseInt(String(timer % 60), 10)

    minutes = minutes < 10 ? '0' + minutes : minutes
    seconds = seconds < 10 ? '0' + seconds : seconds

    --timer

    timerText.value = `${minutes}:${seconds}`
  }

  setInterval(() => {
    countdown()
  }, 1000)

  countdown()
}

onMounted(() => {
  const oneHour = 60 * 60
  startTimer(oneHour)
})
</script>

<template>
  <img :src="gif" class="gif" />

  <div class="container">
    <p class="text-one">Validé à {{ hoursAndMinutes }} le {{ date }}</p>
    <p class="text-two">{{ timerText }}</p>
  </div>
</template>

<style scoped>
.gif {
  position: fixed;
  top: 0;
  left: 0;
}

.container {
  position: relative;
  z-index: 1000;

  font-family: 'Segoe UI';

  top: 820px;
  font-size: 24px;

  left: 200px;

  .text-one {
    color: lightgray;
    margin: 0;
  }

  .text-two {
    padding-left: 118px;
    color: black;
    margin: 0;
    padding-top: 12px;
    font-weight: 800;
  }
}

@font-face {
  font-family: 'Segoe UI';
  font-weight: 200;
  src: local('Segoe UI Light');
}
@font-face {
  font-family: 'Segoe UI';
  font-weight: 300;
  src: local('Segoe UI Semilight');
}
@font-face {
  font-family: 'Segoe UI';
  font-weight: 400;
  src: local('Segoe UI');
}
@font-face {
  font-family: 'Segoe UI';
  font-weight: 600;
  src: local('Segoe UI Semibold');
}
@font-face {
  font-family: 'Segoe UI';
  font-weight: 700;
  src: local('Segoe UI Bold');
}
@font-face {
  font-family: 'Segoe UI';
  font-style: italic;
  font-weight: 400;
  src: local('Segoe UI Italic');
}
@font-face {
  font-family: 'Segoe UI';
  font-style: italic;
  font-weight: 700;
  src: local('Segoe UI Bold Italic');
}
</style>
