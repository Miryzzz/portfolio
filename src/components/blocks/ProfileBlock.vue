<template>
  <section class="flex flex-col justify-between rounded-3xl border border-[#1f1f1f] bg-[#141414] p-6 sm:p-8">
    <div>
      <div class="flex items-start justify-between gap-4">
        <div class="flex h-12 w-12 items-center justify-center rounded-full bg-[#1c1c1c] border border-[#2d2d2d] text-lg font-bold text-sky-400">
          <img
            src="/content/avatar.png"
            alt="Фото профиля"
            class="h-full w-full object-cover rounded-full"
          >
        </div>
        <div class="rounded-full bg-[#1c1c1c] px-4 py-2 text-[10px] sm:text-xs text-gray-400 border border-[#2d2d2d]">
          Frontend-разработчик
        </div>
      </div>
      <div class="mt-12">
        <h1 class="text-3xl sm:text-4xl font-extrabold tracking-tight">
          Матвей
        </h1>
        <p class="mt-4 text-gray-400 text-sm leading-relaxed">
          Студент-программист. Специализируюсь на Vue.js и автоматизации на Python.
        </p>
      </div>
    </div>
    <div class="mt-8 space-y-2 text-[10px] text-gray-500 uppercase tracking-wider">
      <p>📍 Тюмень, Россия</p>
      <p>💻 Чистый код и UI/UX</p>
    </div>
  </section>
</template>
