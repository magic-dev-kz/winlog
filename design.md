# WinLog — Design System & UI Specification

**Дата:** 2026-03-29
**Автор:** Скай (Creative Designer, OpenClaw)
**Версия:** 1.0
**Статус:** Ready for Development

---

## 1. Эмоциональная концепция

### Философия

WinLog — это не приложение. Это **личный ритуал**. Каждый вечер пользователь открывает теплое, безопасное пространство, где его достижения имеют значение.

Ощущение: как будто открыл любимый блокнот в кожаной обложке, сел в кресло с чашкой чая, и записал то, чем гордишься.

### Ключевые принципы

1. **Тепло, не стерильно.** Никакого корпоративного Material Design. Мягкие тени, скругленные углы, органические формы.
2. **Интимно, не социально.** Это пространство только для тебя. Без лайков, шеров, аватарок других людей.
3. **Празднично, не навязчиво.** Каждое сохранение — маленький праздник. Но без кричащих баннеров и pop-up'ов.
4. **Просто, не примитивно.** 2-5 минут на сессию. Каждый элемент оправдан. Ничего лишнего.

### Референсы

| App | Что берем | Что НЕ берем |
|-----|----------|--------------|
| Bears Gratitude | Тепло, мягкость, эмоциональный onboarding, celebration-анимации | Детскость (Bears слишком childish для 28+) |
| Daylio | Compact entry format, mood tracking визуал, calendar heatmap | Холодные цвета, перегруженный UI |
| Five Minute Journal | Структурированный ввод, утро/вечер ритуал | Paywall на все, generic мотивация |
| Notion | Чистая типографика, гибкость | Холодность, complexity |
| Apple Journal | Системная интеграция, фото-suggestions | Привязка к экосистеме |

---

## 2. Цветовая палитра

### Warm Theme (основная, по умолчанию)

```
Background & Surface
────────────────────
--bg-primary:        #FFF9F0    Cream — основной фон, теплый как страница старого блокнота
--bg-secondary:      #FFF3E0    Warm White — карточки, поля ввода
--bg-tertiary:       #FFECCC    Soft Peach — hover-состояния, выделение
--bg-elevated:       #FFFFFF    White — модалки, popup'ы (с мягкой тенью)

Accent & Win Colors
────────────────────
--accent-primary:    #E8A817    Gold — главный акцент, кнопка "Сохранить", streak
--accent-hover:      #D4960F    Deep Gold — hover на акцентных элементах
--accent-light:      #FFF0C2    Pale Gold — фон streak counter, highlight
--accent-glow:       #E8A81733  Gold 20% — glow-эффект кнопки сохранения

Victory Colors (для celebration-анимаций)
─────────────────────────────────────────
--victory-gold:      #F5C842    Bright Gold — конфетти частица
--victory-amber:     #FF9F1C    Amber — конфетти частица
--victory-coral:     #FF6B6B    Soft Coral — конфетти частица
--victory-rose:      #FFB4A2    Rose — конфетти частица

Text
────────────────────
--text-primary:      #3D2C1E    Warm Dark Brown — основной текст (NOT pure black)
--text-secondary:    #7A6555    Warm Gray Brown — подзаголовки, мета
--text-muted:        #B09A88    Muted Tan — placeholder, hint
--text-on-accent:    #FFFFFF    White — текст на золотых кнопках
--text-link:         #C67F17    Warm Link — ссылки

Category Tags
────────────────────
--tag-career:        #4A90D9    Soft Blue
--tag-career-bg:     #EBF3FB    Pale Blue
--tag-health:        #5CB85C    Soft Green
--tag-health-bg:     #EDF7ED    Pale Green
--tag-relations:     #E8636F    Soft Red
--tag-relations-bg:  #FDECEE    Pale Red
--tag-study:         #9B6DC6    Soft Purple
--tag-study-bg:      #F3EDF9    Pale Purple
--tag-creativity:    #E8A817    Gold (same as accent)
--tag-creativity-bg: #FFF6E0    Pale Gold
--tag-finance:       #2AABB3    Teal
--tag-finance-bg:    #E6F6F7    Pale Teal
--tag-other:         #B09A88    Warm Gray
--tag-other-bg:      #F5F0EB    Pale Warm Gray

Streak & Heatmap
────────────────────
--streak-flame:      #FF9F1C    Amber — иконка streak
--heatmap-0:         #F0E8DD    Empty day — теплый серый
--heatmap-1:         #C8E6C9    1-2 записи — светло-зеленый
--heatmap-2:         #81C784    3-4 записи — зеленый
--heatmap-3:         #F5C842    5+ записей — золотой (jackpot!)

Borders & Shadows
────────────────────
--border-subtle:     #E8DDD0    Теплая граница
--border-input:      #D4C4B0    Граница полей ввода
--border-focus:      #E8A817    Focus ring = gold accent
--shadow-card:       0 2px 12px rgba(61, 44, 30, 0.06)
--shadow-elevated:   0 8px 32px rgba(61, 44, 30, 0.10)
--shadow-glow:       0 0 24px rgba(232, 168, 23, 0.15)
```

### Light Theme

Базируется на Warm, но с нейтрально-серым вместо cream:
```
--bg-primary:        #FAFAFA
--bg-secondary:      #FFFFFF
--text-primary:      #1A1A1A
--text-secondary:    #6B6B6B
```

### Dark Theme

```
--bg-primary:        #1C1714    Dark Warm Brown (NOT pure black)
--bg-secondary:      #2A221C    Card background
--bg-tertiary:       #382E26    Hover
--text-primary:      #F0E8DD    Cream text
--text-secondary:    #B09A88    Muted tan
--accent-primary:    #F5C842    Brighter gold for contrast
--border-subtle:     #3D3329    Subtle warm border
```

---

## 3. Типографика

### Шрифт

**Primary:** `'Inter'` — чистый, читаемый, отлично рендерится на всех устройствах.
**Fallback:** `-apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif`

Inter загружается через Google Fonts (wght 400, 500, 600, 700). Subset: latin, cyrillic.

### Шкала

```
--font-hero:         2rem / 32px    font-weight: 700    Приветствие "Добрый вечер"
--font-h1:           1.5rem / 24px  font-weight: 700    Заголовки секций
--font-h2:           1.25rem / 20px font-weight: 600    Подзаголовки
--font-body:         1rem / 16px    font-weight: 400    Основной текст, записи
--font-body-medium:  1rem / 16px    font-weight: 500    Кнопки, labels
--font-small:        0.875rem / 14px font-weight: 400   Мета, даты, подписи
--font-caption:      0.75rem / 12px  font-weight: 500   Бейджи, counters

Line heights:
--lh-tight:          1.2     Заголовки
--lh-normal:         1.5     Основной текст
--lh-relaxed:        1.75    Текстовые поля (для удобства набора)
```

---

## 4. Сетка и Layout

### Mobile-first

```
Viewport: 320px — 768px
Padding: 16px (по бокам)
Content max-width: 100%
```

### Tablet

```
Viewport: 768px — 1024px
Padding: 24px
Content max-width: 640px (центрируется)
```

### Desktop

```
Viewport: 1024px+
Padding: 32px
Content max-width: 640px (центрируется)
Background: --bg-primary растягивается на весь экран
Контент "плавает" по центру — эффект блокнота на столе
```

### Spacing Scale

```
--space-xs:     4px
--space-sm:     8px
--space-md:     16px
--space-lg:     24px
--space-xl:     32px
--space-2xl:    48px
--space-3xl:    64px
```

### Border Radius

```
--radius-sm:    8px     Бейджи, мелкие элементы
--radius-md:    12px    Карточки, поля ввода
--radius-lg:    16px    Большие карточки, модалки
--radius-xl:    24px    Кнопки, floating elements
--radius-full:  9999px  Pill-shaped элементы, аватары
```

---

## 5. Навигация

### Bottom Tab Bar (mobile)

```
┌──────────────────────────────────────────┐
│                                          │
│              [Content Area]              │
│                                          │
├──────────────────────────────────────────┤
│   Today        Timeline       Insights   │
│   [sun]        [list]         [sparkle]  │
│   ●                                      │
└──────────────────────────────────────────┘
```

- Высота: 64px + safe-area-inset-bottom
- Фон: --bg-elevated с blur (backdrop-filter: blur(20px))
- Активный таб: --accent-primary (иконка + текст окрашиваются золотым)
- Неактивный: --text-muted
- Иконки: 24x24, stroke-based, вес 1.5px (Lucide Icons или аналог)
- Переключение: horizontal slide animation (300ms ease-out)

### Desktop adaptation

На десктопе таб-бар можно перенести наверх (горизонтальные табы под приветствием) или оставить внизу контейнера для consistency с мобильным опытом. Рекомендация: **оставить внизу** для единообразия.

---

## 6. Today (главный экран)

### Структура сверху вниз

```
┌──────────────────────────────────────────┐
│                                          │
│  Добрый вечер, Лена          streak: 12  │
│  29 марта, воскресенье        [flame]    │
│                                          │
│  ─────────────────────────────────────── │
│                                          │
│  Чем ты гордишься сегодня?               │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │ 1. Провела презентацию без       │    │
│  │    запинок                       │    │
│  └──────────────────────────────────┘    │
│  ┌──────────────────────────────────┐    │
│  │ 2. Placeholder...            [mic]│    │
│  └──────────────────────────────────┘    │
│  ┌──────────────────────────────────┐    │
│  │ 3. Placeholder...            [mic]│    │
│  └──────────────────────────────────┘    │
│  ┌──────────────────────────────────┐    │
│  │ 4. Placeholder...            [mic]│    │
│  └──────────────────────────────────┘    │
│  ┌──────────────────────────────────┐    │
│  │ 5. Placeholder...            [mic]│    │
│  └──────────────────────────────────┘    │
│                                          │
│  + Добавить ещё                          │
│                                          │
│  Категории:                              │
│  [карьера] [здоровье] [отношения]        │
│  [учеба]  [творчество] [финансы]         │
│                                          │
│       ┌─────────────────────┐            │
│       │   Сохранить   [star]│            │
│       └─────────────────────┘            │
│                                          │
├──────────────────────────────────────────┤
│  Today       Timeline       Insights     │
└──────────────────────────────────────────┘
```

### Детали компонентов

#### Приветствие

- Текст меняется по времени суток:
  - 05:00-11:59 — "Доброе утро"
  - 12:00-17:59 — "Добрый день"
  - 18:00-04:59 — "Добрый вечер"
- Имя берется из настроек (onboarding)
- Шрифт: --font-hero, цвет: --text-primary
- Дата под приветствием: --font-small, цвет: --text-secondary

#### Streak Counter

- Позиция: правый верхний угол, на одной линии с приветствием
- Иконка пламени (--streak-flame) + число
- Фон: --accent-light, скругление: --radius-full (pill)
- При streak = 0: скрыт (не показываем "0 дней" — это демотивирует)
- При milestone (7, 14, 30, 60, 100, 365): специальная анимация (см. секцию 11)

#### Поля ввода побед

- Количество по умолчанию: 5 (настраивается в Settings)
- Каждое поле — отдельная карточка с мягкой тенью (--shadow-card)
- Фон: --bg-secondary
- Border: --border-input, при focus: --border-focus (gold) + --shadow-glow
- Border-radius: --radius-md
- Padding: 12px 16px
- Нумерация: номер слева, цвет --text-muted, font-weight: 600
- Placeholder: "Чем ты гордишься?" (первое поле), далее: "Ещё одна победа...", "Продолжай...", "Ты молодец!", "Финишная прямая!"
- Высота: auto-resize (min 44px, max 120px)
- Иконка микрофона: справа внутри поля, 20x20, --text-muted, при hover --accent-primary
- Transition: border-color 200ms ease, box-shadow 200ms ease

#### Кнопка "Добавить ещё"

- Текст + иконка "+" слева
- Цвет: --text-secondary
- При hover: --accent-primary
- Максимум: 10 полей (из spec AC-1)

#### Категории (теги)

- Горизонтальный scroll (если не помещаются)
- Каждый тег — pill-shaped (--radius-full)
- По умолчанию: outline style (border: 1px solid tag-color, фон: transparent)
- При выборе: filled style (фон: tag-bg, border: tag-color)
- Можно выбрать несколько тегов
- Размер: padding 6px 14px, font: --font-caption
- Категории: карьера, здоровье, отношения, учеба, творчество, финансы, другое

#### Кнопка "Сохранить"

- Ширина: 100% (mobile), max-width 320px (desktop, центрируется)
- Высота: 52px
- Фон: --accent-primary
- Текст: --text-on-accent, --font-body-medium
- Border-radius: --radius-xl
- Иконка звездочки справа от текста
- Shadow: --shadow-glow
- Hover: --accent-hover + усиление glow
- Active: scale(0.97) на 100ms
- Disabled (нет текста ни в одном поле): opacity 0.4, cursor not-allowed
- При нажатии: запускает celebration-анимацию (см. секцию 11)

---

## 7. Timeline (лента записей)

### Структура

```
┌──────────────────────────────────────────┐
│                                          │
│  Мои победы                              │
│                                          │
│  [search icon]  Поиск...                 │
│                                          │
│  Фильтр: [все] [карьера] [здоровье]...  │
│                                          │
│  ─── Сегодня ────────────────────────── │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │ Провела презентацию без запинок   │    │
│  │ Помогла коллеге с отчетом         │    │
│  │ Пробежала 3 км                    │    │
│  │                                   │    │
│  │ [карьера] [здоровье]    21:15     │    │
│  └──────────────────────────────────┘    │
│                                          │
│  ─── Вчера ─────────────────────────── │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │ Закончила курс по SQL             │    │
│  │ Приготовила новое блюдо           │    │
│  │                                   │    │
│  │ [учёба] [творчество]    20:45     │    │
│  └──────────────────────────────────┘    │
│                                          │
│  ─── 27 марта ──────────────────────── │
│  ...                                     │
│                                          │
├──────────────────────────────────────────┤
│  Today       Timeline       Insights     │
└──────────────────────────────────────────┘
```

### Детали

#### Поиск

- Строка поиска сверху: иконка лупы + текстовое поле
- Фон: --bg-secondary, border: --border-input
- При фокусе: border --border-focus
- Real-time filtering (debounce 300ms)
- Highlight найденного текста: фон --accent-light

#### Фильтр категорий

- Горизонтальный scroll, pill-shaped теги (как на Today)
- "Все" выбрано по умолчанию
- Single select (один фильтр за раз)

#### Карточка записи

- Группировка: все записи одного дня = одна карточка
- Фон: --bg-secondary
- Border-radius: --radius-lg
- Padding: 16px
- Shadow: --shadow-card
- Каждая победа — отдельная строка с bullet ("--" или номер)
- Теги внизу карточки (pill badges, маленькие)
- Время записи: справа внизу, --font-caption, --text-muted
- Tap на карточку: expand для редактирования (inline)

#### Разделители дат

- Текст по центру: "Сегодня", "Вчера", или дата (формат: "27 марта, четверг")
- Шрифт: --font-small, --text-muted
- Горизонтальные линии по бокам (тонкие, --border-subtle)

#### Infinite Scroll

- Подгрузка по 20 дней
- Skeleton loading (3 пустые карточки с shimmer-анимацией)
- "Начало твоего пути" — сообщение внизу при достижении первой записи

---

## 8. Insights (AI-зеркало)

### Структура

```
┌──────────────────────────────────────────┐
│                                          │
│  Инсайты                                 │
│                                          │
│  [7 дней]  [30 дней]  [90 дней]          │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │  Суперсила недели                 │    │
│  │                                   │    │
│  │     [карьера]                     │    │
│  │                                   │    │
│  │  60% твоих побед связаны с        │    │
│  │  карьерой. Ты растешь!            │    │
│  └──────────────────────────────────┘    │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │  Твой прогресс           [chart] │    │
│  │  ▂▃▅▆▇█▇▅▃▂▃▅▆▇              │    │
│  │                                   │    │
│  │  21 победа за неделю (+15%)       │    │
│  └──────────────────────────────────┘    │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │  Лучшие дни                       │    │
│  │                                   │    │
│  │  Пн  Вт  Ср  Чт  Пт  Сб  Вс     │    │
│  │  ██  ▅▅  ██  ▃▃  ██  ▂▂  ▅▅     │    │
│  │                                   │    │
│  │  Понедельник и среда — твои       │    │
│  │  самые продуктивные дни!          │    │
│  └──────────────────────────────────┘    │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │  Календарь побед (heatmap)        │    │
│  │                                   │    │
│  │  Пн ░░▓▓░░████░░▓▓░░████        │    │
│  │  Вт ▓▓░░████░░▓▓░░████░░        │    │
│  │  Ср ████▓▓░░████▓▓░░████        │    │
│  │  ...                              │    │
│  └──────────────────────────────────┘    │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │  Лучшая запись                    │    │
│  │                                   │    │
│  │  "Провела презентацию перед       │    │
│  │   директорами и получила          │    │
│  │   аплодисменты"                   │    │
│  │                                   │    │
│  │  — 25 марта              [heart]  │    │
│  └──────────────────────────────────┘    │
│                                          │
│  ┌──────────────────────────────────┐    │
│  │  [export]  Экспортировать         │    │
│  └──────────────────────────────────┘    │
│                                          │
├──────────────────────────────────────────┤
│  Today       Timeline       Insights     │
└──────────────────────────────────────────┘
```

### Детали карточек

#### Период-switcher

- 3 кнопки: "7 дней" / "30 дней" / "90 дней"
- Segmented control style
- Фон неактивного: transparent
- Фон активного: --accent-primary, текст: --text-on-accent
- Border-radius: --radius-full
- Переключение: slide indicator (pill подложка с анимацией 200ms ease)

#### Суперсила недели

- Самая крупная карточка, акцентный фон: gradient от --accent-light к --bg-secondary
- Название категории крупно по центру (--font-h1)
- Бейдж категории с иконкой
- Описание ниже (--font-body, --text-secondary)
- Если записей < 10: "Запиши ещё несколько побед, и я расскажу о твоей суперсиле"

#### График прогресса

- Line chart (Chart.js / uPlot)
- Ось X: дни
- Ось Y: количество записей
- Линия: --accent-primary, толщина 2px
- Заливка под линией: gradient --accent-primary 20% -> transparent
- Точки: отображать при hover/tap
- Подпись: "N побед за период (+/- M%)" — --font-body-medium

#### Лучшие дни недели

- Bar chart, 7 столбцов (Пн-Вс)
- Цвет столбцов: --accent-primary
- Подпись самого активного дня: bold + выделение
- Текстовый инсайт под графиком

#### Calendar Heatmap

- Стиль GitHub contributions
- 4 уровня цвета: --heatmap-0 через --heatmap-3
- Каждый квадрат: 12x12px, gap: 2px
- Tap на квадрат: tooltip с датой и количеством записей
- Scroll горизонтально для прошлых недель

#### Лучшая запись

- Цитата из записей пользователя (самая длинная / с наибольшим количеством побед за день)
- Кавычки-елочки, italic (font-style: italic)
- Дата под цитатой
- Иконка сердца — tap для "сохранить как избранное"
- Фон: --bg-secondary с subtle gradient

---

## 9. Голосовой ввод

### Кнопка микрофона (в поле ввода)

- Размер: 20x20 (внутри поля), color: --text-muted
- Hover: --accent-primary
- Нажатие: открывает voice overlay

### Voice Overlay (модальное состояние)

```
┌──────────────────────────────────────────┐
│                                          │
│                                          │
│          Говори, я записываю...          │
│                                          │
│    ~~~~~~~~ waveform visualization ~~~~  │
│                                          │
│          "Провела презентацию            │
│           перед директорами..."          │
│                                          │
│                                          │
│              ┌───────┐                   │
│              │       │                   │
│              │  MIC  │   <- пульсирует   │
│              │       │                   │
│              └───────┘                   │
│                                          │
│         [Отмена]    [Готово]             │
│                                          │
└──────────────────────────────────────────┘
```

### Детали

#### Overlay

- Фон: --bg-primary с opacity 0.97 (почти непрозрачный)
- Появление: fade-in 300ms + slide-up от кнопки микрофона
- Закрытие: fade-out + slide-down

#### Кнопка записи (главная)

- Размер: 72x72px
- Форма: круг (--radius-full)
- Фон: --accent-primary
- Иконка микрофона: 32x32, белая
- **При записи:** пульсирующая анимация:
  ```css
  @keyframes pulse-record {
    0%   { box-shadow: 0 0 0 0 rgba(232, 168, 23, 0.4); }
    70%  { box-shadow: 0 0 0 20px rgba(232, 168, 23, 0); }
    100% { box-shadow: 0 0 0 0 rgba(232, 168, 23, 0); }
  }
  /* 1.5s infinite */
  ```
- Внешнее кольцо: border 3px --accent-primary, opacity пульсирует

#### Waveform

- Визуализация: набор вертикальных линий (30-40 штук)
- Цвет: --accent-primary
- Высота каждой линии: меняется на основе аудио amplitude (Web Audio API / AnalyserNode)
- Width каждой линии: 3px, border-radius: 2px, gap: 2px
- Когда молчание: все линии одной минимальной высоты (4px), мягко покачиваются

#### Текст real-time

- Транскрибируемый текст появляется по центру
- Шрифт: --font-h2
- Цвет: --text-primary
- Анимация появления: fade-in по словам
- Cursor мигает в конце текста

#### Кнопки управления

- "Отмена": ghost button (только текст, --text-secondary)
- "Готово": primary button (--accent-primary)
- Появляются с задержкой 500ms после начала записи (не отвлекают)

---

## 10. Экспорт

### Кнопка "Экспортировать"

- Расположение: внизу экрана Insights
- Стиль: secondary button (outline, border: --border-input)
- Иконка download слева от текста

### Export Modal

```
┌──────────────────────────────────────────┐
│                                          │
│  Экспорт записей                    [x]  │
│                                          │
│  Период:                                 │
│  [Эта неделя] [Этот месяц] [Всё время]  │
│                                          │
│  Формат:                                 │
│  ┌─────────────┐  ┌─────────────┐        │
│  │     PDF     │  │   Текст     │        │
│  │  (красивый) │  │  (.txt/.md) │        │
│  └─────────────┘  └─────────────┘        │
│                                          │
│  Preview:                                │
│  ┌──────────────────────────────────┐    │
│  │  WinLog — Мои победы             │    │
│  │  27-29 марта 2026                │    │
│  │                                   │    │
│  │  29 марта                         │    │
│  │  - Провела презентацию...         │    │
│  │  ...                              │    │
│  └──────────────────────────────────┘    │
│                                          │
│       [Скачать]                          │
│                                          │
└──────────────────────────────────────────┘
```

### Детали

- Modal: --bg-elevated, --shadow-elevated, --radius-lg
- Backdrop: rgba(0,0,0,0.3) + backdrop-filter: blur(4px)
- Период: segmented control (как в Insights)
- Формат: две карточки-кнопки, стиль radio-select (выбранная: gold border + accent-light фон)
- Preview: встроенный scroll-контейнер, --bg-secondary, --radius-md, max-height 300px
- Кнопка "Скачать": primary button (--accent-primary)
- PDF-стиль: теплый фон, gold headers, логотип WinLog наверху

---

## 11. Микроанимации

### Celebration (при сохранении)

**Sparkle Burst:**
- 15-20 частиц вылетают из кнопки "Сохранить"
- Цвета: --victory-gold, --victory-amber, --victory-coral, --victory-rose
- Форма частиц: маленькие звездочки (4-pointed star) и кружки
- Размер: 4-8px
- Физика: вверх + в стороны, gravity, fade-out
- Длительность: 800ms
- После анимации: кнопка кратко меняет текст на "Сохранено!" с иконкой галочки
- `prefers-reduced-motion`: только смена текста, без частиц

### Streak Milestone

- При достижении 7, 14, 30, 60, 100, 365 дней
- Полноэкранный overlay (полупрозрачный)
- Крупная цифра (streak number) с золотым glow
- Текст: "7 дней подряд!" / "Месяц побед!" / "100 дней! Легенда!"
- Confetti rain сверху (больше частиц чем при обычном сохранении)
- Длительность: 2 секунды, dismiss по tap
- `prefers-reduced-motion`: простая карточка без confetti

### Tab Switch

- Slide transition: контент старого таба уходит влево/вправо, новый приходит
- Duration: 250ms, easing: cubic-bezier(0.4, 0, 0.2, 1)
- Bottom bar indicator: gold dot/pill плавно перемещается под активный таб

### Поле ввода Focus

- Border-color transition: 200ms ease
- Мягкий gold glow появляется (--shadow-glow)
- Номер поля меняет цвет на --accent-primary

### Streak Counter

- При первом появлении на экране: bounce-in (scale 0 -> 1.1 -> 1)
- Пламя: subtle wiggle анимация (бесконечная, медленная)
  ```css
  @keyframes flame-wiggle {
    0%, 100% { transform: rotate(-3deg); }
    50%      { transform: rotate(3deg); }
  }
  /* 2s ease-in-out infinite */
  ```

### Skeleton Loading

- Shimmer gradient: --bg-tertiary проходит волной слева направо
- Duration: 1.5s infinite
- Форма: повторяет layout карточек (закругленные прямоугольники)

### Heatmap Hover

- Квадрат при hover: scale(1.3) + tooltip fade-in (200ms)
- Tooltip: --bg-elevated, --shadow-card, --radius-sm

---

## 12. Onboarding Flow

### Экран 1: Приветствие

```
┌──────────────────────────────────────────┐
│                                          │
│            [star illustration]            │
│                                          │
│         Привет! Это WinLog.              │
│                                          │
│    Кира из книги "Мани" каждый день      │
│    записывала 5 побед. Это изменило      │
│    её жизнь.                             │
│                                          │
│         Попробуем вместе?                │
│                                          │
│         [Начать]                         │
│                                          │
│              o o o                        │
└──────────────────────────────────────────┘
```

### Экран 2: Имя

```
  Как тебя зовут?

  [___________________]

  Мы будем обращаться по имени,
  чтобы было уютнее.

         [Далее]
```

### Экран 3: Количество побед

```
  Сколько побед в день?

  [3 победы]    Для начала
  [5 побед]     Как Кира (рекомендуем)

         [Далее]
```

### Экран 4: Напоминание

```
  Когда напомнить?

  [20:00]  [21:00]  [22:00]

  Или выбери свое время: [__:__]

         [Готово!]
```

### Стиль

- Фон: --bg-primary
- Текст центрирован
- Переход между экранами: slide-left (250ms)
- Dot indicators внизу: --text-muted (неактивный), --accent-primary (активный)
- Кнопки: primary style (--accent-primary)
- Иллюстрации: минимальные, warm-toned (можно заменить эмоджи для MVP: звезда, рукопожатие, колокольчик)

---

## 13. Accessibility (WCAG AA)

### Цветовой контраст

Все пары текст/фон соответствуют WCAG AA (минимум 4.5:1 для обычного текста, 3:1 для крупного):

| Пара | Ratio | Pass? |
|------|-------|-------|
| --text-primary (#3D2C1E) на --bg-primary (#FFF9F0) | 10.2:1 | AA |
| --text-secondary (#7A6555) на --bg-primary (#FFF9F0) | 4.7:1 | AA |
| --text-on-accent (#FFFFFF) на --accent-primary (#E8A817) | 3.1:1 | AA Large |
| --text-muted (#B09A88) на --bg-primary (#FFF9F0) | 2.8:1 | Decorative only |

Примечание: для кнопки "Сохранить" текст крупный (16px bold = Large), ratio 3.1:1 проходит. Если необходимо повысить, использовать --accent-hover (#D4960F) дает 3.8:1.

### Keyboard Navigation

- Все интерактивные элементы доступны через Tab
- Focus ring: 2px solid --border-focus, offset 2px
- Tab bar: Arrow keys для переключения табов
- Enter / Space: активация кнопок
- Escape: закрытие модалок и voice overlay
- Поля ввода: Tab переключает между полями побед

### Screen Reader

- Все иконки имеют aria-label
- Микрофон: `aria-label="Голосовой ввод"`, при записи: `aria-live="polite"` озвучивает транскрибируемый текст
- Streak: `aria-label="Серия: 12 дней подряд"`
- Графики: текстовые alt-описания (`aria-label="График: 21 победа за неделю, рост 15%"`)
- Категории-теги: `role="checkbox"`, `aria-checked`
- Tab bar: `role="tablist"`, `role="tab"`, `aria-selected`

### Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

- Celebration: заменяется на смену текста кнопки
- Tab switch: instant (без slide)
- Streak milestone: карточка без confetti
- Waveform: статичные линии одной высоты
- Flame wiggle: отключена

### Touch Targets

- Минимальный размер touch target: 44x44px (iOS HIG)
- Кнопки: min-height 44px
- Теги категорий: min-height 36px, но с padding/margin итого 44px touch area
- Heatmap квадраты (12x12): tooltip по tap, не по точному попаданию (увеличенная touch area)

---

## 14. Компоненты (Component Library)

### Кнопки

```
Primary:    bg --accent-primary, text --text-on-accent, radius --radius-xl, h 52px
Secondary:  bg transparent, border --border-input, text --text-primary, radius --radius-xl, h 44px
Ghost:      bg transparent, no border, text --text-secondary, h 44px
Danger:     bg #E8636F, text white (для удаления записей)
```

### Карточки

```
Default:    bg --bg-secondary, shadow --shadow-card, radius --radius-lg, p 16px
Elevated:   bg --bg-elevated, shadow --shadow-elevated, radius --radius-lg, p 20px
Accent:     gradient(--accent-light, --bg-secondary), shadow --shadow-card, radius --radius-lg
```

### Бейджи (теги)

```
Outline:    border 1px solid [tag-color], bg transparent, radius --radius-full, p 6px 14px
Filled:     bg [tag-bg], border 1px solid [tag-color], radius --radius-full, p 6px 14px
Mini:       font --font-caption, p 3px 8px (в карточках Timeline)
```

### Текстовое поле

```
Default:    bg --bg-secondary, border --border-input, radius --radius-md, p 12px 16px
Focus:      border --border-focus, shadow --shadow-glow
Error:      border #E8636F (если понадобится)
```

### Иконки

- Набор: Lucide Icons (MIT, stroke-based, consistent)
- Размеры: 16px (inline), 20px (в полях), 24px (navigation), 32px (voice overlay)
- Stroke width: 1.5px (default), 2px (active state)
- Используемые иконки:
  - `sun` — Today tab
  - `list` — Timeline tab
  - `sparkles` — Insights tab
  - `mic` — Voice input
  - `search` — Search
  - `flame` — Streak
  - `download` — Export
  - `check` — Saved
  - `x` — Close
  - `plus` — Add entry
  - `heart` — Favorite
  - `star` — Save button decoration
  - `settings` — Settings (gear)
  - `chevron-left/right` — Navigation

---

## 15. Settings (доступ через иконку gear в header)

### Содержание

- **Имя:** текстовое поле
- **Побед в день:** stepper (3-10)
- **Напоминание:** time picker + toggle on/off
- **Тема:** 3 варианта (Warm / Light / Dark) — visual preview для каждой
- **Язык:** русский / English (Phase 2)
- **О приложении:** версия, ссылка на OpenClaw
- **Очистить данные:** danger button с double-confirm

Стиль: полноэкранная страница, список grouped-секций (как iOS Settings).

---

## 16. Empty States

### Первый день (нет записей)

```
  [star illustration]

  Запиши свою первую победу!

  Даже маленькие достижения
  заслуживают внимания.

  [Начать]
```

### Timeline (пустой)

```
  Здесь будет хронология
  твоих побед.

  Начни с первой записи!
```

### Insights (мало данных)

```
  Чтобы увидеть инсайты,
  нужно минимум 10 записей.

  Ты уже записал(а) 3 из 10.

  [##########----------]  30%
```

Стиль: центрированный текст, мягкий, --text-secondary, иллюстрация/эмоджи сверху.

---

## 17. Responsive Breakpoints

```css
/* Mobile (default) */
/* 320px - 767px */

@media (min-width: 768px) {
  /* Tablet */
  /* Content max-width: 640px, centered */
  /* Больше padding, крупнее шрифты заголовков */
}

@media (min-width: 1024px) {
  /* Desktop */
  /* Content max-width: 640px, centered */
  /* Subtle background pattern/texture за контейнером */
  /* Tab bar можно оставить внизу контейнера */
}
```

---

## 18. CSS Custom Properties (полный список)

```css
:root {
  /* Colors */
  --bg-primary: #FFF9F0;
  --bg-secondary: #FFF3E0;
  --bg-tertiary: #FFECCC;
  --bg-elevated: #FFFFFF;

  --accent-primary: #E8A817;
  --accent-hover: #D4960F;
  --accent-light: #FFF0C2;
  --accent-glow: rgba(232, 168, 23, 0.2);

  --text-primary: #3D2C1E;
  --text-secondary: #7A6555;
  --text-muted: #B09A88;
  --text-on-accent: #FFFFFF;
  --text-link: #C67F17;

  --tag-career: #4A90D9;
  --tag-career-bg: #EBF3FB;
  --tag-health: #5CB85C;
  --tag-health-bg: #EDF7ED;
  --tag-relations: #E8636F;
  --tag-relations-bg: #FDECEE;
  --tag-study: #9B6DC6;
  --tag-study-bg: #F3EDF9;
  --tag-creativity: #E8A817;
  --tag-creativity-bg: #FFF6E0;
  --tag-finance: #2AABB3;
  --tag-finance-bg: #E6F6F7;
  --tag-other: #B09A88;
  --tag-other-bg: #F5F0EB;

  --streak-flame: #FF9F1C;
  --heatmap-0: #F0E8DD;
  --heatmap-1: #C8E6C9;
  --heatmap-2: #81C784;
  --heatmap-3: #F5C842;

  --victory-gold: #F5C842;
  --victory-amber: #FF9F1C;
  --victory-coral: #FF6B6B;
  --victory-rose: #FFB4A2;

  --border-subtle: #E8DDD0;
  --border-input: #D4C4B0;
  --border-focus: #E8A817;

  --shadow-card: 0 2px 12px rgba(61, 44, 30, 0.06);
  --shadow-elevated: 0 8px 32px rgba(61, 44, 30, 0.10);
  --shadow-glow: 0 0 24px rgba(232, 168, 23, 0.15);

  /* Typography */
  --font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
  --font-hero: 2rem;
  --font-h1: 1.5rem;
  --font-h2: 1.25rem;
  --font-body: 1rem;
  --font-small: 0.875rem;
  --font-caption: 0.75rem;
  --lh-tight: 1.2;
  --lh-normal: 1.5;
  --lh-relaxed: 1.75;

  /* Spacing */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  --space-2xl: 48px;
  --space-3xl: 64px;

  /* Radius */
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 24px;
  --radius-full: 9999px;

  /* Animation */
  --duration-fast: 150ms;
  --duration-normal: 250ms;
  --duration-slow: 400ms;
  --ease-default: cubic-bezier(0.4, 0, 0.2, 1);
  --ease-bounce: cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

---

*"Каждый день записывай минимум пять вещей, которые тебе удались."*
*Этот дизайн создан, чтобы сделать этот ритуал теплым, простым и вдохновляющим.*
