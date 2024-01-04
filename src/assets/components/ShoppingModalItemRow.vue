<script setup>
const props = defineProps(['name']);

const buy = () => {
  playCashSound();
};

const playCashSound = async () => {
  try {
    const module = await import('@/assets/cash.mp3');
    const audio = new Audio(module.default);
    audio.addEventListener('canplaythrough', () => {
      audio.play();
    });
  } catch (error) {
    console.error('Erro ao carregar o arquivo de áudio:', error);
  }
};
</script>

<template>
  <main class="text-white flex justify-between items-center">
    <div class="flex items-center">
      <img :src="`/src/assets/images/${props.name}.png`" class="w-32" />
      <div class="flex flex-col ml-2">
        <div class="flex gap-2 items-end">
          <p class="text-xl">{{ props.name.toUpperCase() }}</p>
          <p class="text-sm text-cyan-500">| YOU HAVE (0)</p>
        </div>
        <p class="text-gray-400">$1 PER SECOND</p>
        <p class="text-yellow-500 text-sm">PRICE $10</p>
      </div>
    </div>
    <div
      class="border-white border rounded-full h-fit p-2 px-3 transition-all active:scale-90 hover:bg-slate-800 cursor-pointer"
      @click="buy(props.name)"
    >
      <p class="text-xs">BUY</p>
    </div>
  </main>
</template>
