# Портфолио Матвея

Одностраничный сайт-портфолио на Vue 3 + Vite + Tailwind CSS.

## Стек

- Vue 3 (`<script setup>`)
- Vite
- Tailwind CSS 4

## Локальный запуск

```bash
npm install
npm run dev
```

Приложение будет доступно на адресе, который выведет Vite (обычно `http://localhost:5173`).

## Сборка

```bash
npm run build
npm run preview
```

## Структура

- `src/App.vue` - сборка страницы из блоков
- `src/components/blocks/` - UI-блоки (профиль, проекты, стек, контакты, резюме, модалка)
- `src/data/portfolioData.js` - контент портфолио
- `public/content/` - статические изображения и резюме
