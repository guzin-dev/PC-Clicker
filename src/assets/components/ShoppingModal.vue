<script setup>
import ShoppingModalItemRow from '@/assets/components/ShoppingModalItemRow.vue';
import { ref, onMounted } from 'vue';
</script>
<template>
  <main
    @click.self="$emit('close')"
    class="w-screen h-screen bg-black bg-opacity-50 absolute z-20 font-lucky flex justify-center items-center"
  >
    <div class="w-[34rem] h-[34rem] bg-zinc-900 flex flex-col rounded-md p-5">
      <div class="text-white flex justify-between items-center">
        <div class="flex items-end gap-2 justify-center">
          <p class="text-2xl">SHOP</p>
          <p class="text-yellow-500">CURRENT MONEY $0</p>
        </div>
        <p
          @click="$emit('close')"
          class="cursor-pointer active:scale-90 hover:opacity-50 hover:text-red-700 transition-all"
        >
          X
        </p>
      </div>
      <div class="h-[0.1px] w-full bg-zinc-600"></div>
      <div class="divide-y divide-zinc-700 gap-2 flex flex-col">
        <ShoppingModalItemRow name="mouse" />
        <ShoppingModalItemRow name="keyboard" />
        <ShoppingModalItemRow name="case" />
        <ShoppingModalItemRow name="monitor" />
      </div>
    </div>
  </main>
</template>
