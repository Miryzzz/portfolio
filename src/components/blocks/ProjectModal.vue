<template>
  <Transition name="fade">
    <div v-if="project" class="fixed inset-0 z-50 flex items-center justify-center p-4" @keydown.esc="emit('close')">
      <div class="absolute inset-0 bg-black/80 backdrop-blur-md" @click="emit('close')"></div>

      <div
        class="relative w-full max-w-2xl overflow-hidden rounded-3xl border border-[#2d2d2d] bg-[#141414] shadow-2xl"
        role="dialog"
        aria-modal="true"
        :aria-labelledby="dialogTitleId"
      >
        <div class="h-48 w-full overflow-hidden border-b border-[#2d2d2d] bg-[#0a0a0a] sm:h-64">
          <img :src="project.image" :alt="project.title" class="h-full w-full object-cover opacity-80">
        </div>

        <div class="p-6 sm:p-8">
          <div class="mb-6 flex items-start justify-between">
            <div>
              <h2 :id="dialogTitleId" class="text-2xl font-bold text-white sm:text-3xl">{{ project.title }}</h2>
              <div class="mt-3 flex flex-wrap gap-2">
                <span
                  v-for="tag in project.tags"
                  :key="tag"
                  class="rounded-full border border-sky-500/20 bg-sky-500/10 px-2 py-1 text-[9px] font-bold uppercase tracking-wider text-sky-400"
                >
                  {{ tag }}
                </span>
              </div>
            </div>
            <button
              ref="closeButtonRef"
              @click="emit('close')"
              class="text-gray-500 transition-colors hover:text-white focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-sky-400"
              aria-label="Закрыть окно"
              type="button"
            >
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
            </button>
          </div>

          <div class="prose prose-invert max-w-none">
            <p class="text-sm leading-relaxed text-gray-400 sm:text-base">{{ project.fullDesc }}</p>
            <div v-if="project.features" class="mt-6">
              <h4 class="mb-2 text-xs font-bold uppercase tracking-widest text-white">Ключевые особенности:</h4>
              <ul class="grid grid-cols-1 gap-2 text-xs text-gray-500 sm:grid-cols-2 sm:text-sm">
                <li v-for="feature in project.features" :key="feature" class="flex items-center gap-2">
                  <span class="h-1 w-1 rounded-full bg-sky-400"></span> {{ feature }}
                </li>
              </ul>
            </div>
          </div>

          <div class="mt-10 flex gap-4">
            <a
              v-if="project.link && project.link !== '#'"
              :href="project.link"
              target="_blank"
              rel="noopener noreferrer"
              class="flex-1 rounded-xl bg-white py-4 text-center text-sm font-bold uppercase text-black transition-all hover:bg-sky-400"
            >
              Открыть проект
            </a>
            <a
              v-if="project.github && project.github !== '#'"
              :href="project.github"
              target="_blank"
              rel="noopener noreferrer"
              class="flex-1 rounded-xl border border-[#2d2d2d] bg-[#1c1c1c] py-4 text-center text-sm font-bold uppercase text-white transition-all hover:bg-[#222]"
            >
              Исходный код
            </a>
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup>
import { nextTick, ref, watch } from "vue";

const props = defineProps({
  project: {
    type: Object,
    default: null,
  },
});

const emit = defineEmits(["close"]);
const closeButtonRef = ref(null);
const lastFocusedElement = ref(null);
const dialogTitleId = "project-modal-title";

watch(
  () => props.project,
  async (project) => {
    if (project) {
      lastFocusedElement.value = document.activeElement;
      await nextTick();
      closeButtonRef.value?.focus();
      return;
    }

    const elementToRestore = lastFocusedElement.value;
    if (elementToRestore instanceof HTMLElement) {
      elementToRestore.focus();
    }
  },
);
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
