<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
const dateTime = new Date('2025-07-03T09:00:00');
const timeLeft = ref(timeRemaining());
let timer = null

function timeRemaining() {
  const now = new Date();
  const total = dateTime - now;

  const seconds = Math.floor((total / 1000) % 60);
  const minutes = Math.floor((total / 1000 / 60) % 60);
  const hours = Math.floor((total / (1000 * 60 * 60)) % 24);
  const days = Math.floor(total / (1000 * 60 * 60 * 24));

  return {
    total,
    days,
    hours,
    minutes,
    seconds
  };
}

onMounted(() => {
  timer = setInterval(() => {
    timeLeft.value = timeRemaining();
  }, 1000);
});

onUnmounted(() => {
  clearInterval(timer);
});
</script>

<template>
<div v-if="timeLeft.total > 0">
    <div class="text-center mb-10">
      <h2 class="text-5xl">Countdown to F1</h2>
      <p>(When I set off from my house, dependent on how cooperative the kids are)</p>
    </div>
    <div class="flex justify-center gap-4">
 <div class="flex flex-col items-center w-20">
        <span class="bg-gray-800 text-white font-mono text-3xl py-2 w-full rounded-md shadow-inner shadow-black/30 text-center">
          {{ timeLeft.days }}
        </span>
        <span class="mt-2 text-sm text-white uppercase tracking-wide">Days</span>
      </div>
      <div class="flex flex-col items-center w-20">
        <span class="bg-gray-800 text-white font-mono text-3xl py-2 w-full rounded-md shadow-inner shadow-black/30 text-center">
          {{ timeLeft.hours }}
        </span>
        <span class="mt-2 text-sm text-white uppercase tracking-wide">Hours</span>
      </div>
      <div class="flex flex-col items-center w-20">
        <span class="bg-gray-800 text-white font-mono text-3xl py-2 w-full rounded-md shadow-inner shadow-black/30 text-center">
          {{ timeLeft.minutes }}
        </span>
        <span class="mt-2 text-sm text-white uppercase tracking-wide">Minutes</span>
      </div>
      <div class="flex flex-col items-center w-20">
        <span class="bg-gray-800 text-white font-mono text-3xl py-2 w-full rounded-md shadow-inner shadow-black/30 text-center">
          {{ timeLeft.seconds }}
        </span>
        <span class="mt-2 text-sm text-white uppercase tracking-wide">Seconds</span>
      </div>
    </div>
  </div>
  <div v-else>
    <h2>Countdown Complete!</h2>
  </div>
  <iframe class="opacity-0 invisible absolute top-[-999999px]" 
  width="100%" 
  height="166" 
  scrolling="no" 
  frameborder="no" 
  allow="autoplay" 
  src="https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/ramirez-471538183/formula-1-theme-brian-tyler&auto_play=true&loop=true">
</iframe>
</template>
