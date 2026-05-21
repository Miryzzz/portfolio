<template>
  <div class="min-h-screen w-full bg-black text-white selection:bg-white/10 font-sans overflow-x-hidden">
    <div class="relative h-full w-full">
      <div class="pointer-events-none absolute inset-0 bg-[radial-gradient(circle_at_top_left,_rgba(56,189,248,0.12),_transparent_30%),radial-gradient(circle_at_top_right,_rgba(96,165,250,0.08),_transparent_25%),radial-gradient(circle_at_bottom_left,_rgba(16,185,129,0.06),_transparent_28%)]" />

      <div class="relative mx-auto h-full w-full px-4 py-6 sm:px-6 lg:px-8 flex flex-col gap-6 max-w-7xl">
        <div class="grid grid-cols-1 xl:grid-cols-[320px_1fr_320px] gap-6">
          <ProfileBlock />
          <div class="grid grid-cols-1 gap-6">
            <SocialsBlock :socials="socials" />
            <ResumeBlock />
          </div>
          <StackBlock :stack="stack" />
        </div>

        <ProjectsBlock
          :projects="projects"
          :show-full-list="showFullList"
          @toggle-list="toggleProjectList"
          @open-project="openProject"
        />
      </div>
    </div>

    <ProjectModal :project="selectedProject" @close="closeModal" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import ProfileBlock from "./components/blocks/ProfileBlock.vue";
import ProjectModal from "./components/blocks/ProjectModal.vue";
import ProjectsBlock from "./components/blocks/ProjectsBlock.vue";
import ResumeBlock from "./components/blocks/ResumeBlock.vue";
import SocialsBlock from "./components/blocks/SocialsBlock.vue";
import StackBlock from "./components/blocks/StackBlock.vue";
import { projects, socials, stack } from "./data/portfolioData";

const selectedProject = ref(null);
const showFullList = ref(false);

const toggleProjectList = () => {
  showFullList.value = !showFullList.value;
};

const openProject = (project) => {
  selectedProject.value = project;
  document.body.style.overflow = "hidden";
};

const closeModal = () => {
  selectedProject.value = null;
  document.body.style.overflow = "";
};
</script>
