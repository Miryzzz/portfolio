<template>
  <section class="flex h-full flex-col rounded-3xl border border-[#1f1f1f] bg-[#141414] p-6 sm:p-8 shadow-2xl">
    <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between mb-8 gap-4">
      <h2 class="text-2xl sm:text-3xl font-extrabold tracking-tight">Мои работы</h2>
      <button
        @click="emit('toggle-list')"
        class="rounded-full border border-[#262626] bg-[#1c1c1c] px-6 py-2 text-[10px] text-gray-400 font-bold hover:text-white hover:border-sky-500/50 transition-all uppercase"
      >
        {{ showFullList ? "Свернуть" : "Все проекты" }}
      </button>
    </div>

    <div class="grid flex-1 content-start grid-cols-1 gap-4 md:grid-cols-2 2xl:grid-cols-3">
      <article
        v-for="project in visibleProjects"
        :key="project.title"
        class="rounded-2xl border border-[#262626] bg-[#1c1c1c] transition-all hover:border-sky-500/30 hover:bg-[#1f1f1f]"
      >
        <button
          type="button"
          @click="emit('open-project', project)"
          class="group w-full cursor-pointer p-6 text-left focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-sky-400 focus-visible:ring-offset-2 focus-visible:ring-offset-[#1c1c1c]"
          :aria-label="`Открыть проект ${project.title}`"
        >
          <div class="mb-4 flex items-start justify-between">
            <h3 class="text-lg font-bold text-gray-100 transition-colors group-hover:text-sky-400">
              {{ project.title }}
            </h3>
            <svg class="text-gray-700 transition-all group-hover:-translate-y-1 group-hover:translate-x-1 group-hover:text-sky-400" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="7" y1="17" x2="17" y2="7"></line><polyline points="7 7 17 7 17 17"></polyline></svg>
          </div>
          <p class="text-sm leading-relaxed text-gray-500">{{ project.desc }}</p>
        </button>
      </article>
    </div>
  </section>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  projects: {
    type: Array,
    required: true,
  },
  showFullList: {
    type: Boolean,
    required: true,
  },
});

const emit = defineEmits(["toggle-list", "open-project"]);

const visibleProjects = computed(() =>
  props.showFullList ? props.projects : props.projects.slice(0, 3),
);
</script>
