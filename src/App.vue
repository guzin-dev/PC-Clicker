<script setup>
import { ref, watch } from 'vue';
import ShoppingModal from '@/assets/components/ShoppingModal.vue';

const money = ref(0);

const addMoney = (value) => {
  money.value = money.value + value;
  playClickSound();
};

const isShopOpened = ref(false);

const playClickSound = async () => {
  try {
    const module = await import('@/assets/click.mp3');
    const audio = new Audio(module.default);
    audio.addEventListener('canplaythrough', () => {
      audio.play();
    });
  } catch (error) {
    console.error('Erro ao carregar o arquivo de áudio:', error);
  }
};

watch(money, (val) => {
  localStorage.setItem('money', val);
});
</script>

<template>
  <main class="bg-zinc-900 w-screen h-screen font-lucky flex flex-col justify-between">
    <ShoppingModal v-if="isShopOpened" @close="isShopOpened = false" />
    <div class="text-center mt-6">
      <p class="text-white text-4xl">PC CLICKER</p>
      <p class="text-gray-400 text-xl">THE GAME</p>
    </div>
    <div class="flex items-center flex-col justify-center">
      <p class="text-gray-400">CLICK TO EARN MONEY</p>
      <div
        class="relative flex justify-center items-center w-32 mt-5 transition-all cursor-pointer hover:opacity-55 active:scale-90"
        @click="addMoney(1)"
      >
        <img class="z-10" src="./assets/images/processador.png" />
        <div class="absolute w-32 h-32 shadow-lg shadow-white top-0 bg-white opacity-50 rounded-full"></div>
      </div>
    </div>
    <div class="text-center w-full flex flex-col items-center">
      <p class="text-yellow-500 text-2xl">CURRENT MONEY ${{ money }}</p>
      <p class="text-white">MONEY PER SECOND $0</p>
      <div
        class="flex text-white px-12 py-2 border justify-center items-center active:scale-90 border-white rounded-full w-fit mt-2 cursor-pointer transition-all hover:bg-slate-800 mb-6"
        @click="isShopOpened = true"
      >
        <p>OPEN SHOP</p>
      </div>
    </div>
  </main>
</template>
