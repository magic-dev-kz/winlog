# Дневник Успеха — Competitive Research

**Дата:** 2026-03-29
**Автор:** Саня (PM, OpenClaw)
**Статус:** Complete

---

## 1. Вдохновение

Книга "Мани, или Азбука денег" (Бодо Шефер) — девочка Кира ведет дневник успеха: каждый день записывает 5 вещей, которыми гордится. Фокус на ДОСТИЖЕНИЯХ, а не на благодарности.

**Ключевое отличие от gratitude journals:** благодарность = пассивная ("спасибо что есть солнце"), успех = активная ("я сделал это"). Разная психология, разная аудитория, разный retention.

---

## 2. Прямые конкуренты (Daily Wins / Achievement)

### 2.1 3 Wins (iOS)
- **Цена:** Free с IAP
- **Рейтинг:** ~4.5
- **Суть:** Записать 3 победы в день. Calendar view с цветовой кодировкой (зеленый = 3+ побед). Apple Watch, Siri Shortcuts, CSV export, iCloud sync.
- **Сильные стороны:** Простота, Apple Watch, нет перегруженного UI.
- **Слабые стороны:** Нет голосового ввода, нет AI, нет визуализации трендов, нет PDF export, нет эмоционального дизайна. Утилита, не продукт.
- **Оценка угрозы:** 6/10 — наш ближайший конкурент по концепции, но feature gap огромный.

### 2.2 Winly: Daily Wins Tracker (iOS)
- **Цена:** Free
- **Суть:** Логирование побед без набора текста (тап), streak calendar.
- **Слабые стороны:** Слишком упрощенный. Нет глубины, нет рефлексии, нет AI.
- **Оценка угрозы:** 3/10 — другой сегмент (quick logging vs. journaling).

### 2.3 ProudOf: Daily Wins Tracker (Android)
- **Цена:** Free
- **Суть:** Трекер достижений с метафорой "дерева прогресса".
- **Сильные стороны:** Визуальная метафора роста — хорошая идея.
- **Слабые стороны:** Только Android, базовый функционал.
- **Оценка угрозы:** 2/10.

### 2.4 Wins Journal (iOS)
- **Суть:** Трекер целей + история достижений.
- **Слабые стороны:** Goal-oriented, не journal-oriented. Разные задачи.

---

## 3. Gratitude Journal Apps (косвенные конкуренты)

### 3.1 Bears Gratitude (Apple Design Award 2024 — Delight & Fun)
- **Цена:** Free, ~$4 за unlimited версию. Без агрессивных paywall.
- **Рейтинг:** Высокий (ADA winner)
- **Суть:** 100+ рисованных медведей, стикеры за достижения, мини-статьи, пастельная палитра.
- **Что украсть:** Эмоциональный дизайн, ощущение тепла, hand-drawn персонажи. Монетизация без раздражения.
- **Что НЕ делать:** Фокус только на gratitude, нет AI, нет voice, нет trends.

### 3.2 Five Minute Journal (Intelligent Change)
- **Цена:** Freemium, подписка (monthly/yearly/lifetime). Переход на подписку вызвал волну негатива.
- **Рейтинг:** 4.7 (но скандал с потерей данных)
- **Суть:** Утренние/вечерние промпты, mood tracker, фото/видео, кастомные вопросы.
- **Что украсть:** Структура утро/вечер. Вечерние "wins" — прямо наша тема.
- **Критические баги:** Потеря данных при обновлении (3+ года записей пропали). Наш roadmap: offline-first, local backup.

### 3.3 Day One
- **Цена:** $49.99/год (только annual). Самый дорогой journaling app.
- **Рейтинг:** 4.5, но негатив растет.
- **Отзыв январь 2026:** "$50 a year is absolutely bonkers for a journaling app"
- **Проблемы:** Нет поиска внутри записей (!), нет кастомизации (цвета, шрифты), sync issues, потеря данных, плохая поддержка.
- **Что украсть:** End-to-end encryption, book printing (как premium feature).
- **Что НЕ делать:** $50/год за базовый журнал. Нет кастомизации. Потеря данных.

### 3.4 Presently (Android, Open Source)
- **Цена:** Бесплатно навсегда, без рекламы.
- **Рейтинг:** 4.9 на Google Play
- **Суть:** Минималистичный gratitude journal на Kotlin. Цитаты, напоминания, fingerprint lock.
- **Что украсть:** Open source подход, чистый дизайн, privacy-first.
- **Слабые стороны:** Только Android, нет AI, нет voice, нет analytics.

### 3.5 Reflectly
- **Суть:** Mood log, gratitude prompts, streak tracking, AI-driven prompts.
- **Сильные стороны:** AI-промпты, позитивное переосмысление.

### 3.6 Daylio
- **Рейтинг:** Лучший retention в категории — Day 30 retention ~40% (vs. 22% у Finch).
- **Суть:** Mood + habits с иконками вместо текста. Visual stats.
- **Что украсть:** Подход к retention. Минимальный friction для записи.

---

## 4. Что бесит людей в journaling apps

| Проблема | Источник | Наше решение |
|----------|----------|--------------|
| **Потеря данных** при обновлении/синке | Five Minute Journal, Day One | Offline-first, localStorage + экспорт |
| **Дорогая подписка** за базовый функционал | Day One ($50/yr) | Freemium: core бесплатно, AI/export = premium |
| **Aggressive upsells** | Journey (1.6★ на Trustpilot) | Честный paywall, не popup-спам |
| **Нет кастомизации** | Day One | Темы, цвета, шрифты |
| **Sync issues** между устройствами | Day One, Five Minute Journal | PWA + localStorage (нет sync проблем для MVP) |
| **Нет поиска** внутри записей | Day One | Full-text search по записям |
| **Ограниченная поддержка браузеров** для voice | Web Speech API | Fallback на текстовый ввод, Progressive Enhancement |
| **Privacy concerns** | Reddit threads | Все данные локально, zero-knowledge |
| **Базовый feature set** | Pixel Journal, Winly | Voice + AI + визуализация + export |

---

## 5. Свободная ниша

### Матрица позиционирования

```
                    Глубокий анализ
                         |
                    [НАША НИША]
                         |
    Минимализм ——————————+—————————— Богатый UI
                         |
                   Быстрый лог
```

**Свободная ниша:** "Achievement journal с AI-инсайтами и голосовым вводом"

- Gratitude apps = пассивная рефлексия, нет AI, нет voice
- Wins trackers = quick logging, нет глубины, нет анализа
- Full journals (Day One) = generic, дорого, sync issues
- **Дневник Успеха = фокусированный на достижениях journal с AI и voice, privacy-first, доступный**

### Почему "дневник успеха" != "дневник благодарности"

| Аспект | Gratitude | Success |
|--------|-----------|---------|
| Психология | Благодарность за то что есть | Гордость за то что СДЕЛАЛ |
| Действие | Пассивное замечание | Активное достижение |
| Мотивация | Снижение тревоги | Рост уверенности |
| Retention driver | Привычка | Прогресс + привычка |
| AI value | Низкий (что анализировать?) | Высокий (паттерны, тренды, рекомендации) |

---

## 6. Retention benchmarks

- Daylio: 40% Day-30 retention (лучший в категории)
- Finch: 22% Day-30 retention
- Среднее journaling app: 10-15% Day-30
- **Наша цель: 30%+ Day-30 retention** через streaks + AI insights + прогресс-визуализацию

### Что работает для retention:
- Streaks: пользователи с 7+ дней серией в 2.3x чаще возвращаются ежедневно (данные Duolingo)
- Streaks + milestones: -35% churn за 30 дней vs. non-gamified
- Gamification усиливает retention на 22% в среднем
- Немедленная обратная связь (points, badges, encouraging messages) после каждой записи

---

## 7. Технические findings

### Web Speech API
- **Поддержка:** Chrome + Chromium-based (Edge). НЕ поддерживается в Firefox/Safari полноценно.
- **Ограничения:** Client-side only, плохие голоса для не-английских языков, нет server-side visibility.
- **Решение:** Progressive Enhancement — voice как бонус, текст как fallback. Whisper.js (local) как альтернатива для offline.

---

## 8. Ценовые бенчмарки

| App | Модель | Цена |
|-----|--------|------|
| Bears Gratitude | Free + $4 unlock | Одноразовая покупка |
| Five Minute Journal | Freemium + подписка | Monthly/Yearly/Lifetime |
| Day One | Subscription only | $49.99/год |
| Presently | 100% бесплатно | Open source |
| 3 Wins | Free + IAP | — |
| Journey | Subscription | Aggressive upsells |

**Наша стратегия:** Free core + $2.99/мес или $19.99/год за AI + export + themes.

---

## Sources

- [Apple Design Awards 2024](https://www.apple.com/newsroom/2024/06/apple-announces-winners-of-the-2024-apple-design-awards/)
- [Bears Gratitude — Apple Developer](https://developer.apple.com/news/?id=i74v3f4r)
- [Bears Gratitude — App Store](https://apps.apple.com/us/app/bears-gratitude/id6443609622)
- [Five Minute Journal — App Store](https://apps.apple.com/us/app/5-minute-journal-daily-diary/id1062945251)
- [Five Minute Journal Pricing](https://www.intelligentchange.com/blogs/support/five-minute-journal-app-cost)
- [Day One Pricing](https://dayoneapp.com/pricing/)
- [Day One Review 2024](https://www.choosingtherapy.com/dayone-app-review/)
- [Day One Alternatives 2026](https://blog.mylifenote.ai/day-one-journal-alternative/)
- [3 Wins — App Store](https://apps.apple.com/us/app/3-wins/id970221138)
- [Winly — App Store](https://apps.apple.com/us/app/winly-daily-wins-tracker/id6757267664)
- [ProudOf — Google Play](https://play.google.com/store/apps/details?id=com.hhoorriiaa.firstapp)
- [Presently](https://presently-app.firebaseapp.com/)
- [Best AI Journaling Apps 2026](https://www.aijournalapp.ai/blog/best-ai-journal-apps/)
- [Best Digital Journal Apps 2026](https://blog.planwiz.app/best-digital-journal-apps/)
- [Web Speech API — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API)
- [Gamification Strategies — Storyly](https://www.storyly.io/post/gamification-strategies-to-increase-app-engagement)
- [Streaks for Gamification — Plotline](https://www.plotline.so/blog/streaks-for-gamification-in-mobile-apps/)
- [Gamification Guide — RevenueCat](https://www.revenuecat.com/blog/growth/gamification-in-apps-complete-guide/)
- [Bears Gratitude Showcase — ScreensDesign](https://screensdesign.com/showcase/bears-gratitude)
