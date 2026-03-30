# Дневник Успеха — Product Specification

**Дата:** 2026-03-29
**Автор:** Саня (PM, OpenClaw)
**Версия:** 1.0
**Статус:** Ready for Review

---

## 1. Название

**WinLog** (рабочее)

Варианты: WinLog / ProudDay / DailyWin / Кира (отсылка к книге)

Критерии выбора: короткое, запоминающееся, передает суть (wins + logging), свободный домен, не конфликтует с существующими apps.

---

## 2. Persona

### Основная: Лена, 28 лет, Junior PM в IT-компании

- Синдром самозванца. Чувствует что "недостаточно хороша", хотя объективно растет.
- Читала "Мани" Шефера или подобное — идея дневника успеха резонирует.
- Вечером листает Instagram вместо рефлексии.
- Хочет: видеть свой прогресс, перестать обесценивать достижения.
- Боится: что забросит через неделю (как все предыдущие дневники).
- Платит за: Notion ($10/мес), Headspace ($70/год). Ready to pay за полезное.
- Устройства: iPhone + MacBook. Основное использование — телефон вечером в кровати.

### Вторичная: Артем, 35 лет, предприниматель

- Ведет бизнес, много задач, мало рефлексии.
- Хочет фиксировать бизнес-wins для мотивации и отчета инвесторам.
- Голосовой ввод критичен — нет времени печатать.
- Хочет экспортировать quarterly review в PDF.

---

## 3. Позиционирование

> **WinLog — дневник достижений с AI-инсайтами. Записывай победы. Видь рост. Верь в себя.**

Не gratitude journal (пассивно). Не task tracker (утилитарно). Не generic journal (размыто).
WinLog = фокусированный инструмент роста уверенности через фиксацию побед.

---

## 4. Главная функция (Core Loop)

```
Вечер → Открыл app → Записал 3-5 побед (текст/голос) →
→ Получил AI-инсайт → Увидел streak → Закрыл с улыбкой
```

**Время на сессию:** 2-5 минут (не больше).
**Ключевой момент:** "Ага-эффект" от AI-инсайта. Не generic "отличная работа!", а конкретный паттерн: "За последние 2 недели 60% твоих побед связаны с коммуникацией — это твоя суперсила".

---

## 5. Изюм (Differentiator)

### "AI-зеркало" — локальный AI-анализ без API

Раз в неделю (Sunday Review) app анализирует записи и показывает:
1. **Категории побед** — автоматическая классификация (работа, здоровье, отношения, творчество, учеба)
2. **Тренды** — "на этой неделе у тебя больше побед в категории 'здоровье' чем на прошлой"
3. **Суперсила** — "твоя #1 категория за месяц: коммуникация"
4. **Паттерн дней** — "среда и пятница — твои самые продуктивные дни"
5. **Прогресс** — "количество записей выросло на 20% по сравнению с прошлым месяцем"

**Реализация без API:** keyword extraction + категоризация через словари + статистика. Все локально. Zero data leaks. Zero API costs.

---

## 6. Acceptance Criteria (12 штук)

### Core (MVP)

**AC-1: Ежедневная запись**
- GIVEN пользователь открывает app
- WHEN нажимает "+" или "Записать победу"
- THEN видит поле ввода с плейсхолдером "Чем ты гордишься сегодня?"
- AND может добавить от 1 до 10 записей за день
- AND каждая запись имеет timestamp и дату

**AC-2: Голосовой ввод**
- GIVEN пользователь нажимает иконку микрофона
- WHEN говорит текст
- THEN текст транскрибируется в реальном времени через Web Speech API
- AND пользователь может отредактировать результат перед сохранением
- AND если браузер не поддерживает Speech API — иконка микрофона скрыта (Progressive Enhancement)

**AC-3: Streak tracking**
- GIVEN пользователь записал хотя бы 1 победу сегодня
- WHEN открывает app на следующий день
- THEN видит текущий streak (N дней подряд)
- AND streak отображается на главном экране с анимацией при достижении milestone (7, 14, 30, 60, 100, 365)
- AND пропуск 1 дня = streak reset (без "freeze" в MVP)

**AC-4: Calendar view**
- GIVEN пользователь открывает вкладку "Календарь"
- WHEN смотрит текущий месяц
- THEN видит цветовую карту: пустой день = серый, 1-2 записи = светло-зеленый, 3+ = ярко-зеленый, 5+ = золотой
- AND тап на день = список побед этого дня

**AC-5: Поиск по записям**
- GIVEN пользователь вводит текст в строку поиска
- WHEN совпадение найдено
- THEN отображаются записи с highlighted совпадениями
- AND поиск работает по всем полям (текст победы, дата)

**AC-6: Данные — offline-first**
- GIVEN пользователь работает с app
- WHEN нет интернета
- THEN все функции работают (запись, чтение, поиск, calendar)
- AND данные хранятся в localStorage/IndexedDB
- AND данные НИКОГДА не отправляются на сервер без явного согласия

### AI & Analytics (Premium)

**AC-7: Категоризация побед**
- GIVEN пользователь записал 10+ побед
- WHEN открывает вкладку "Аналитика"
- THEN видит pie chart с автоматически определенными категориями
- AND категории: Работа, Здоровье, Отношения, Творчество, Учеба, Финансы, Другое
- AND категоризация работает локально через keyword matching (без API)

**AC-8: Weekly AI Review (Sunday Review)**
- GIVEN прошла неделя с 3+ записями
- WHEN пользователь открывает app в воскресенье (или по запросу)
- THEN видит карточку "Обзор недели" с: top категория, количество побед, тренд vs прошлая неделя, "суперсила недели"
- AND инсайт формулируется позитивно и конкретно

**AC-9: Визуализация прогресса**
- GIVEN пользователь использует app 2+ недели
- WHEN открывает "Аналитика"
- THEN видит: line chart побед по неделям, bar chart по категориям, streak history
- AND все графики интерактивные (тап = детали)

### Export & Customization

**AC-10: Экспорт в PDF**
- GIVEN пользователь нажимает "Экспорт"
- WHEN выбирает период (неделя/месяц/произвольный)
- THEN получает красиво оформленный PDF с записями, статистикой и графиками
- AND PDF генерируется локально (html2pdf.js или jsPDF)

**AC-11: Экспорт в текст**
- GIVEN пользователь нажимает "Экспорт" → "Текст"
- WHEN выбирает период
- THEN скачивается .txt/.md файл со всеми записями и датами

**AC-12: Темы и настройки**
- GIVEN пользователь открывает настройки
- WHEN выбирает тему
- THEN может переключить: Light / Dark / Warm (теплая пастель a la Bears Gratitude)
- AND может настроить время напоминания (push notification через Service Worker)
- AND может изменить количество "целевых побед" в день (по умолчанию 5, по Шеферу)

---

## 7. User Flow (Happy Path)

```
1. Первый запуск
   └→ Onboarding: "Кира из книги 'Мани' каждый день записывала 5 побед.
       Это изменило её жизнь. Попробуем?"
   └→ Выбор: 3 или 5 побед в день
   └→ Настройка напоминания (вечер)

2. Ежедневное использование (2-5 мин)
   └→ Push в 21:00: "Время побед! 🏆"
   └→ Открыл → записал победы (текст/голос) → увидел streak → закрыл
   └→ Milestone анимация при 7, 14, 30 днях

3. Еженедельный ритуал (Sunday Review)
   └→ Карточка "Обзор недели"
   └→ AI-инсайты, тренды, суперсила
   └→ Мотивация продолжать

4. Ежемесячный ритуал
   └→ Monthly Report с полной аналитикой
   └→ Опция экспорта в PDF

5. Retention loop
   └→ Streak → не хочу терять
   └→ AI insights → интересно что будет на следующей неделе
   └→ Progress visualization → вижу рост → горжусь собой
```

---

## 8. Технические требования

### Stack
- **Frontend:** Vanilla JS + HTML + CSS (PWA). Без фреймворков для скорости и размера.
- **Storage:** IndexedDB (через Dexie.js) для записей, localStorage для настроек.
- **Voice:** Web Speech API (SpeechRecognition) с fallback.
- **Charts:** Chart.js (lightweight, 60KB gzipped) или uPlot (10KB).
- **PDF Export:** jsPDF + html2canvas.
- **Push:** Service Worker + Notification API.
- **AI (локальный):** Keyword extraction + dictionary-based categorization. Без ML, без API calls.

### Архитектура
```
PWA (installable)
├── index.html (SPA)
├── service-worker.js (offline + push)
├── js/
│   ├── app.js (router, state)
│   ├── storage.js (IndexedDB via Dexie)
│   ├── voice.js (Web Speech API)
│   ├── analytics.js (categorization, trends)
│   ├── export.js (PDF, text)
│   └── charts.js (visualization)
├── css/
│   ├── themes/ (light, dark, warm)
│   └── animations.css
└── manifest.json
```

### Требования к производительности
- First Contentful Paint: < 1s
- Time to Interactive: < 2s
- Bundle size: < 200KB gzipped (total)
- Работает offline после первого визита
- 60fps анимации

### Браузерная поддержка
- Chrome 90+, Edge 90+, Safari 15+ (без voice), Firefox 100+ (без voice)
- iOS Safari (PWA ограничения: нет push до iOS 16.4+)
- Android Chrome (полная поддержка PWA)

---

## 9. Anti-Scope (что НЕ делаем)

| Фича | Почему нет |
|-------|-----------|
| Социальные функции (шеринг, лента друзей) | Privacy-first. Дневник = личное пространство. |
| Cloud sync | Сложность + privacy + sync bugs (см. Day One, 5MJ). MVP = one device. |
| Native app (iOS/Android) | PWA покрывает 90% use cases. Native = x10 затрат. |
| ML/LLM для анализа | Overkill для MVP. Dictionary-based categorization достаточно. LLM = phase 2. |
| Streak freeze | Мотивация через честность, не через хаки. |
| Фото/видео в записях | Усложняет storage. Phase 2. |
| Multi-language AI | MVP = русский + английский. |
| Интеграция с HealthKit/Calendar | Phase 2. |
| Monetization (paywall) | Phase 1 = полностью бесплатно. Paywall = phase 2 после product-market fit. |

---

## 10. Метрики успеха

| Метрика | Target (3 мес) | Gold (6 мес) |
|---------|----------------|--------------|
| DAU | 100 | 500 |
| Day-7 retention | 40% | 50% |
| Day-30 retention | 25% | 35% |
| Avg session length | 3 min | 4 min |
| Avg entries/day | 3 | 4 |
| Streak > 7 days | 30% users | 45% users |
| Voice usage | 15% sessions | 25% sessions |
| NPS | 40 | 60 |

---

## 11. Roadmap

### Phase 1 — MVP (2 недели)
- Core loop: запись побед (текст + голос)
- Streak tracking + calendar view
- Offline-first (IndexedDB)
- Базовая тема (warm)
- PWA (installable)
- Push-напоминания

### Phase 2 — Analytics (2 недели)
- AI-категоризация (keyword-based)
- Weekly Review карточка
- Charts (линейный + pie)
- Поиск по записям

### Phase 3 — Export & Polish (1 неделя)
- PDF export
- Text export
- Dark theme + theme switcher
- Milestone animations
- Onboarding flow

### Phase 4 — Growth (ongoing)
- Landing page + SEO
- Product Hunt launch
- App Store (через Capacitor/TWA, если нужно)
- Cloud sync (optional, end-to-end encrypted)
- LLM-based insights (local, через WebLLM или Gemini Nano)
- Photo/video в записях
- HealthKit/Calendar интеграция

---

## 12. Конкурентное преимущество (moat)

| Мы | 3 Wins | Five Minute Journal | Day One | Bears Gratitude |
|----|--------|---------------------|---------|-----------------|
| Голосовой ввод | Нет | Нет | Нет | Нет |
| AI-инсайты | Нет | Нет | Базовые ($50/yr) | Нет |
| Визуализация прогресса | Calendar only | Нет | Базовая | Нет |
| Offline-first | iCloud | Cloud | Cloud | Local |
| Privacy (zero-knowledge) | iCloud | Cloud | Cloud | Local |
| PDF export | CSV | Нет | Есть | Нет |
| Бесплатно (core) | Да | Нет | Нет | Почти |
| Фокус на ДОСТИЖЕНИЯХ | Да | Gratitude | Generic | Gratitude |
| Эмоциональный дизайн | Нет | Средний | Нет | Да (лучший) |

**Наш moat:** единственный achievement journal с голосовым вводом + AI-инсайтами + privacy-first + бесплатный core. Ни один конкурент не закрывает все 4.

---

## 13. Риски и митигация

| Риск | Вероятность | Импакт | Митигация |
|------|-------------|--------|-----------|
| Web Speech API ненадежен | Средняя | Средний | Fallback на текст, progressive enhancement |
| Keyword categorization неточна | Средняя | Низкий | Пользователь может поправить категорию вручную |
| PWA ограничения на iOS | Высокая | Средний | Фокус на Android + desktop, iOS = text-only mode |
| Low retention (как у всех journals) | Высокая | Высокий | Streaks + AI insights + milestone celebrations |
| IndexedDB limits | Низкая | Высокий | ~50MB = 10+ лет записей. Export как backup. |

---

## 14. Definition of Done (для MVP)

- [ ] Можно записать 5 побед за < 3 минуты
- [ ] Голосовой ввод работает в Chrome (desktop + Android)
- [ ] Streak отображается корректно
- [ ] Calendar view с цветовой кодировкой
- [ ] Данные сохраняются после закрытия браузера
- [ ] Работает offline
- [ ] Installable как PWA
- [ ] Push-напоминание приходит в настроенное время
- [ ] Lighthouse Performance: 95+
- [ ] Lighthouse PWA: 100
- [ ] Accessibility: AA level
- [ ] Bundle size < 200KB gzipped

---

*"Каждый день записывай минимум пять вещей, которые тебе удались. Так ты научишься быть довольной собой и своей жизнью."*
— Бодо Шефер, "Мани, или Азбука денег"
