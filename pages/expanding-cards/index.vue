<script setup lang="ts">
import cards from "~/pages/expanding-cards/data";

const activeIndex = ref<number | null>(0)
onMounted(() => {
  // 此时可以安全访问 document
  document.title = '拓展盒子'
})
</script>

<template>
  <div class="flex min-h-screen items-center justify-center">
    <div class="mx-10 flex w-full gap-5">
      <div
          v-for="(card, index) in cards"
          :key="index"
          :style="{ backgroundImage: 'url(' + card.url + ')' }"
          class="relative h-[80vh] flex-[0.5] rounded-lg bg-cover bg-center transition-all duration-700 ease-in hover:cursor-pointer"
          :class="{ 'flex-[5]': index === activeIndex }"
          @click="activeIndex = index"
      >
        <h3
            class="absolute bottom-20 left-20 text-2xl font-bold text-white opacity-0"
            :class="{ 'opacity-100 delay-[400ms] transition-opacity duration-300 ease-in': index === activeIndex }"
        >
          {{ card.name }}
        </h3>
      </div>
    </div>
  </div>
</template>