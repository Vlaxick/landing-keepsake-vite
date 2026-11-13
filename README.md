# Vite Pug Template

Шаблон для швидкого старту проєктів з використанням **Vite**, **Pug**, та **SCSS**.  
Структура оптимізована для компонентного підходу: Pug-компоненти, SCSS-модулі та гнучка система підключення стилів.

---

## 🔧 Вимоги до середовища

Для запуску проєкту необхідно мати встановлений Node.js (версія 20 або новіша) та npm.

### 1. Перевірка наявності Node.js і npm

```bash
node -v
npm -v
```

Якщо у консолі з’явилися версії (наприклад v20.10.0), усе гаразд ✅

### 2. Встановлення Node.js

Якщо Node.js не встановлено — завантажте останню LTS-версію з офіційного сайту:
👉 https://nodejs.org

Після встановлення перевірте знову:

```bash
node -v
npm -v
```

## 🚀 Запуск проєкту

### 1. Встановлення залежностей

```bash
npm install
```

### 2. Режим розробки

```bash
npm run dev
```

Проєкт запуститься локально (зазвичай на [http://localhost:5173](http://localhost:5173))  
Файли автоматично оновлюються при зміні коду.

### 3. Збірка для продакшну

```bash
npm run build
```

Готові файли з’являться в директорії `dist/`.

### 4. Перегляд зібраної версії

```bash
npm run preview
```

---

## 🧩 Структура проєкту

```
src/
 ├─ assets/              # зображення, шрифти, інші ресурси
 ├─ components/          # Pug-компоненти (header, footer, content, ...)
 ├─ data/                # файли з даними
 ├─ includes/            # head, meta, fonts (частини шаблону)
 ├─ layouts/             # основні макети сторінок
 ├─ pages/               # сторінки сайту
 ├─ styles/              # SCSS-структура
 │   ├─ base/            # базові стилі: reset, типографія
 │   ├─ components/      # стилі компонентів
 │   ├─ layout/          # сітка, секції
 │   ├─ utils/           # змінні, міксіни
 │   └─ main.scss        # головний файл стилів
 └─ vite.config.js       # налаштування Vite + Vituum
```

---

## 📝 Робота з Pug

### 📄 Мінімальний приклад сторінки (`src/pages/index.pug`)

```pug
doctype html
html(lang='en')
  include ../includes/head.pug

  body
    include ../components/header.pug

    main.page
      section.intro
        h1 Hello, Vite + Pug + SCSS!
        p Це приклад простої сторінки з компонентами.

    include ../components/footer.pug
```

---

### 🧱 Приклад компонентів

#### `src/components/header.pug`

```pug
header.site-header
  h2 Логотип або назва сайту
```

#### `src/components/footer.pug`

```pug
footer.site-footer
  p © 2025 Мій шаблон на Vite + Pug
```

#### `src/includes/head.pug`

```pug
head
  meta(charset='utf-8')
  meta(name='viewport', content='width=device-width, initial-scale=1')
  title Vite Pug Template
  link(rel='stylesheet', href='/src/styles/main.scss')
```

---

## 🎨 Робота з SCSS

### 📂 Структура стилів

Головний файл — `src/styles/main.scss`

```scss
@use 'utils/index' as *;
@use 'base/index' as *;
@use 'layout/index' as *;
@use 'components/index' as *;
```

---

### 📄 Мінімальний приклад `src/styles/utils/_variables.scss`

```scss
$color-bg: #f5f5f5;
$color-text: #222;
$font-main: 'Inter', sans-serif;
```

---

### 📄 Мінімальний приклад `src/styles/main.scss`

```scss
@use 'utils/variables' as *;

body {
  font-family: $font-main;
  background-color: $color-bg;
  color: $color-text;
  margin: 0;
  padding: 0;
}

.site-header,
.site-footer {
  text-align: center;
  padding: 1.5rem;
  background: #ddd;
}

.intro {
  text-align: center;
  padding: 3rem 1rem;
}
```

---

## 🧠 Корисні поради

- Усі компоненти підключай через `include`.
- SCSS імпортуй лише у `main.scss`, а не у Pug-файлах.
- Додавай зображення до `src/assets/` і використовуй їх у коді як:
  ```pug
  img(src='/src/assets/logo.png', alt='Logo')
  ```

---

## 📦 Використані пакети

| Пакет                                                                            | Опис                      |
| -------------------------------------------------------------------------------- | ------------------------- |
| [Vite](https://vitejs.dev/)                                                      | Швидкий білдер проєктів   |
| [Vituum](https://vituum.dev/)                                                    | Плагін для шаблонізаторів |
| [@vituum/vite-plugin-pug](https://www.npmjs.com/package/@vituum/vite-plugin-pug) | Підтримка Pug             |
| [Sass](https://sass-lang.com/)                                                   | Препроцесор стилів        |

## PostCSS та підтримувані браузери (лабораторна №9, завдання 4)

Vite компілює SCSS, передає CSS плагіну Autoprefixer через `postcss.config.js`, а під час production-збірки мініфікує результат. Цільові браузери визначає `.browserslistrc`: останні дві версії Chrome, Firefox, Edge, Safari та iOS Safari.

```bash
npx browserslist
npx autoprefixer --info
npm run dev
npm run build
```

У режимі розробки для фільтрів портфоліо в DevTools можна побачити `-webkit-user-select`, який Autoprefixer додає до `user-select`. Префікси залежать від цільових браузерів: наприклад, Safari їх потребує для цієї властивості, а останні версії Chrome — ні. Мініфікований CSS після збірки знаходиться у `dist/assets/`.

## Адаптивні зображення (лабораторна №9, завдання 5)

Вихідні файли знаходяться в `src/assets/images/`. Команда `npm run images` за допомогою Sharp генерує у `src/assets/images/generated/` два розміри кожного зображення: AVIF, WebP і JPEG (або PNG для прозорих джерел). Створені файли збережені в репозиторії, тому збірка працює без повторної конвертації.

Міксин `picture` виводить формати в порядку AVIF → WebP → запасний JPEG, з `srcset`, `sizes`, розмірами, `alt`, `decoding` і відкладеним завантаженням. Vite додає хеші до імен файлів і залишає зображення окремими файлами, щоб не завантажувати їх усі разом з HTML. Посилання на повнорозмірні роботи використовують `public/images/`.

Джерела з попередньої роботи невеликі: роботи — 358 × 282 px, прев’ю журналу — 150 × 150 px. Тому створено варіанти 179/358 px і 75/150 px без штучного збільшення; чіткість обмежена якістю оригіналів. Під час перевірки в DevTools → Network можна прокрутити до журналу та побачити, як браузер завантажує відповідний AVIF або WebP.

## Якість коду (лабораторна №9, завдання 6)

- `npm run format` форматує проєкт через Prettier і плагін Pug.
- `npm run lint` перевіряє SCSS через Stylelint та форматування через Prettier. Окремо можна запустити `npm run lint:styles` або `npm run lint:format`.
- Після `npm install` або `npm ci` скрипт `prepare` налаштовує Husky. Перед комітом lint-staged перевіряє й форматує лише додані до коміту файли: для SCSS запускає Stylelint з автовиправленням і Prettier, для Pug, JS, JSON і Markdown — Prettier. Помилки, які не можна виправити автоматично, блокують коміт.
- Конфігурація Stylelint дозволяє БЕМ-імена, обмежує вкладеність трьома рівнями та забороняє ID-селектори й `!important`. Правило про початковий `_` у шляхах Sass вимкнено для явного підключення `_index.scss`: так уже запущений Vite не звертається до старих видалених `index.scss` після перейменування.
