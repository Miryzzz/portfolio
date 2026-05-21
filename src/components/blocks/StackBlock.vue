<template>
  <section class="rounded-3xl border border-[#1f1f1f] bg-[#141414] p-6 sm:p-8">
    <h2 class="mb-8 text-xl font-bold tracking-tight sm:text-2xl">Технологии</h2>
    <div class="grid grid-cols-1 gap-3">
      <div
        v-for="tech in stack"
        :key="tech.name"
        class="group flex items-center gap-4 rounded-xl border border-[#262626] bg-[#1c1c1c] px-4 py-3 transition-all hover:border-sky-500/30"
      >
        <div class="flex h-10 w-10 shrink-0 items-center justify-center rounded-lg border border-[#333333] bg-[#262626] transition-all group-hover:border-sky-500/50 group-hover:bg-sky-500/10">
          <div class="h-5 w-5 text-gray-400 transition-colors group-hover:text-white" v-html="tech.svg"></div>
        </div>
        <span class="text-sm font-semibold text-gray-300 transition-colors group-hover:text-white">{{ tech.name }}</span>
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({
  stack: {
    type: Array,
    required: true,
  },
});
</script>
