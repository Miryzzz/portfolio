<template>
  <section class="rounded-3xl border border-[#1f1f1f] bg-[#141414] p-6 sm:p-8">
    <div class="flex items-center justify-between mb-6">
      <h2 class="text-xl sm:text-2xl font-bold tracking-tight">Связаться со мной</h2>
      <span class="text-[9px] text-gray-600 uppercase tracking-[0.2em]">Контакты</span>
    </div>
    <div class="grid grid-cols-3 gap-3">
      <a
        v-for="item in socials"
        :key="item.name"
        :href="item.href"
        target="_blank"
        rel="noopener noreferrer"
        class="group flex flex-col items-center justify-center py-5 rounded-2xl border border-[#262626] bg-[#1c1c1c] transition-all hover:border-sky-500/50 hover:bg-[#1f1f1f]"
      >
        <div class="w-6 h-6 mb-2 text-gray-400 group-hover:text-white transition-colors" v-html="item.svg"></div>
        <span class="text-[9px] text-gray-500 uppercase group-hover:text-white transition-colors">
          {{ item.name }}
        </span>
      </a>
    </div>
  </section>
</template>

<script setup>
defineProps({
  socials: {
    type: Array,
    required: true,
  },
});
</script>
