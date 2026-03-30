# WinLog -- Аудит (Нэш)

**Дата:** 2026-03-29
**Аудитор:** Нэш, QA-тестировщик OpenClaw
**Артефакты:** spec.md (12 AC), design.md, index.html (92KB single-file SPA)
**Оценка: 7.2 / 10**

---

## AC проверка (все 12)

### AC-1: Ежедневная запись -- PASS (с замечаниями)

- [x] Кнопка "Записать победу" / поля ввода отображаются при открытии
- [x] Плейсхолдер "Чем ты гордишься?" присутствует
- [x] Можно добавить от 1 до 10 записей (addMoreBtn, лимит 10)
- [x] Каждая запись имеет timestamp (`createdAt: new Date().toISOString()`) и дату (`date: dateKey(...)`)
- **Minor:** При добавлении полей через "Добавить ещё" нет анимации (design.md предписывает мягкую анимацию). Не блокер, но дизайн-рассинхрон.

### AC-2: Голосовой ввод -- PASS (с замечаниями)

- [x] Иконка микрофона скрыта при отсутствии Web Speech API (`if (SpeechAvailable)` в `addWinField`)
- [x] Текст транскрибируется в реальном времени (`interimResults = true`)
- [x] Пользователь может отредактировать результат -- текст вставляется в textarea после нажатия "Готово"
- [x] Progressive Enhancement: нет API = нет кнопок, app полностью работоспособен
- **Minor:** `speechRec.onerror = () => {}` -- ошибки голосового ввода молча подавляются. Пользователь не получит feedback, если микрофон заблокирован в браузере.

### AC-3: Streak tracking -- PASS (с замечаниями)

- [x] Streak подсчитывается корректно (`calculateStreak()`)
- [x] Отображается на главном экране с badge
- [x] Milestone анимация при 7, 14, 30, 60, 100, 365
- [x] Пропуск 1 дня = reset (проверено: если сегодня нет записей, проверяется вчера; если и вчера нет -- streak = 0)
- **Major:** Streak-алгоритм содержит логический баг. Если пользователь записал победы сегодня И вчера, но позавчера пропустил, streak будет 2. Однако если пользователь ЕЩЁ не записал сегодня, алгоритм начнёт проверку с yesterday. Если вчера есть, а позавчера нет -- streak будет 1, хотя пользователь мог бы считать что его streak "жив" (он ещё не закончил сегодняшний день). Это не баг по спеке (спека говорит "пропуск 1 дня = reset"), но UX-мягко: утром streak может показаться "потерянным" до первой записи. Оставляю как **Minor UX issue**, не нарушает спеку.

### AC-4: Calendar view -- PARTIAL PASS

- [x] Цветовая карта в Insights (heatmap): 0 = серый, 1-2 = светло-зелёный, 3-4 = зелёный, 5+ = золотой
- **Major:** Спека требует **отдельную вкладку "Календарь"**. В реализации Calendar view встроен в Insights как heatmap-карточка. Навигации нет -- нельзя нажать на день и увидеть список побед этого дня (AC-4: "тап на день = список побед этого дня"). Heatmap показывает только tooltip с количеством, а не записи.
- **Missing:** Переключение месяцев в calendar view. В heatmap зафиксировано 90 дней.

### AC-5: Поиск по записям -- PASS

- [x] Строка поиска в Timeline
- [x] Real-time filtering с debounce 300ms
- [x] Highlighted совпадения через `<mark>` (`highlightText` функция)
- [x] Поиск работает по тексту победы
- **Minor:** Поиск НЕ работает по дате (спека: "поиск работает по всем полям (текст победы, дата)"). Если набрать "марта" -- ничего не найдётся, потому что фильтрация идёт только по `w.text`.

### AC-6: Данные -- offline-first -- PASS

- [x] IndexedDB как основное хранилище
- [x] localStorage fallback
- [x] Все функции работают без сервера (запись, чтение, поиск, calendar)
- [x] Данные НИКОГДА не отправляются на сервер
- **Note:** Нет Service Worker, поэтому сам HTML/CSS/JS не будет доступен offline после первого визита. Это нарушает PWA-требование из спеки (секция 8: "Работает offline после первого визита"). Для статического single-file HTML это менее критично, но формально SW отсутствует.

### AC-7: Категоризация побед -- PASS

- [x] Pie chart -- ОТСУТСТВУЕТ. Спека требует "pie chart с автоматически определенными категориями". Реализовано только через Superpower card (текстовое описание top-категории).
- **Major:** Pie chart НЕ реализован. Есть line chart, bar chart, heatmap, но не pie chart.
- [x] Категоризация работает локально через keyword matching
- [x] 7 категорий: Работа, Здоровье, Отношения, Учёба, Творчество, Финансы, Другое

### AC-8: Weekly AI Review (Sunday Review) -- PARTIAL PASS

- [x] Карточка "Суперсила" с top-категорией
- [x] Количество побед за период
- [x] Инсайт формулируется позитивно
- **Major:** Нет отдельной "Sunday Review" карточки, которая появляется именно в воскресенье. Insights доступны всегда и не привязаны к дню недели. Спека: "WHEN пользователь открывает app в воскресенье (или по запросу)". Нет специального Sunday-триггера.
- **Missing:** Тренд "vs прошлая неделя" не реализован. Спека: "тренд vs прошлая неделя". Insights показывают данные за период, но не сравнивают с предыдущим.

### AC-9: Визуализация прогресса -- PASS (с замечаниями)

- [x] Line chart побед по дням -- есть
- [x] Bar chart по дням недели -- есть
- [x] Heatmap (streak history) -- есть
- **Minor:** Спека требует "интерактивные графики (тап = детали)". Line chart и bar chart НЕ интерактивны -- нет кликов, нет tooltip. Только heatmap имеет tooltip.

### AC-10: Экспорт в PDF -- PARTIAL PASS

- [x] Кнопка "Экспорт" есть
- [x] Выбор периода (неделя/месяц/всё)
- **Major:** PDF генерируется через `window.open()` + `window.print()`. Это не PDF-экспорт, а печать HTML-страницы. Спека: "PDF генерируется локально (html2pdf.js или jsPDF)". Нет реального PDF-файла, нет графиков/статистики в экспорте. Пользователь получает окно печати браузера.
- **Missing:** "Красиво оформленный PDF с записями, статистикой и графиками" -- графики и статистика отсутствуют в print-версии.

### AC-11: Экспорт в текст -- PASS

- [x] Кнопка "Текст (.txt)" в модалке экспорта
- [x] Выбор периода
- [x] Скачивается .txt файл со всеми записями и датами
- [x] Blob + URL.createObjectURL -- работает корректно

### AC-12: Темы и настройки -- PARTIAL PASS

- [x] Light / Dark / Warm темы -- реализованы и переключаются
- [x] Можно изменить количество побед в день (3-10)
- **Critical:** Настройка времени напоминания НЕ реализована. Нет Service Worker, нет Notification API, нет push-напоминаний. Спека: "может настроить время напоминания (push notification через Service Worker)".
- **Missing:** Нет поля для времени напоминания в Settings panel.

---

## Баги

### Critical (2)

**C-1: Отсутствие Service Worker и Push Notifications**
- Спека явно требует: push-напоминания через Service Worker (AC-12), offline after first visit (AC-6), installable PWA (Definition of Done).
- Реализация: нет `service-worker.js`, нет `manifest.json`, нет Notification API.
- Impact: app не installable как PWA, не работает offline (сам HTML недоступен), нет напоминаний.
- Это самый крупный пропуск в реализации.

**C-2: XSS через поиск в Timeline**
- Функция `highlightText` (строка 1571):
  ```js
  function highlightText(text, query) {
    const escaped = escapeHtml(text);
    const q = escapeHtml(query);
    const regex = new RegExp(`(${q.replace(/[.*+?^${}()|[\]\\]/g, '\\$&')})`, 'gi');
    return escaped.replace(regex, '<mark>$1</mark>');
  }
  ```
  Текст экранируется через `escapeHtml`, но результат вставляется через `li.innerHTML`. Если запись содержит текст вроде `&lt;script&gt;`, то `escapeHtml` превратит его в `&amp;lt;script&amp;gt;`, и после `innerHTML` отобразится как `&lt;script&gt;` -- это корректно. **Перепроверка: XSS защита ЕСТЬ для записей (textContent при обычном рендере, escapeHtml при поиске).** Однако:
  - `greetingText` на строке 1319: `document.getElementById('greetingText').textContent = ...` -- используется `textContent`, безопасно.
  - `escapeHtml` в milestone (строка 1437): `escapeHtml(text)` -- безопасно.
  - **Всё же есть уязвимость:** `entriesToText` используется для `preview.textContent` -- безопасно. Для PDF-экспорта используется `escapeHtml(text)` -- безопасно.

  **Переквалифицирую C-2 в отсутствие:** XSS-защита в целом АДЕКВАТНА. `escapeHtml` применяется корректно. Снимаю Critical.

  **Замена C-2:** Переношу отсутствие Pie Chart (AC-7) в Critical, т.к. это явное требование спеки.

**C-2 (revised): Отсутствие Pie Chart для категоризации**
- AC-7 явно требует: "видит pie chart с автоматически определенными категориями".
- Реализация: категоризация работает, но визуально -- только текстовая карточка "Суперсила". Pie chart не реализован вообще.

### Major (5)

**M-1: Calendar view вместо полноценной вкладки -- только heatmap в Insights**
- AC-4 требует тап на день = список побед. Текущий heatmap показывает только tooltip с числом.

**M-2: PDF экспорт через window.print() вместо реального PDF**
- AC-10 требует jsPDF/html2pdf.js. Текущий подход не генерирует файл, зависит от диалога печати браузера, не содержит графики.

**M-3: Нет Weekly Review (Sunday Review) как отдельной функции**
- AC-8 требует специальную карточку, привязанную к воскресенью и сравнение с прошлой неделей.

**M-4: Поиск не работает по дате**
- AC-5: "поиск работает по всем полям (текст победы, дата)". Текущий поиск -- только по тексту.

**M-5: Focus trap отсутствует в модалках и overlay**
- Export modal, Voice overlay, Settings panel, Milestone overlay -- ни один не реализует focus trap.
- Tab-навигация позволяет "проваливаться" за пределы модального окна к элементам под ним.
- Escape закрытие -- ЕСТЬ (корректно), но это не заменяет focus trap.

### Minor (9)

**m-1: Onboarding -- имя необязательно, но Step 1 не валидирует**
- На шаге 1 (имя) кнопка "Далее" активна даже с пустым полем. Пользователь может пройти без имени -- это допустимо по спеке (имя необязательно), но UX дизайн предполагает мягкое напоминание.

**m-2: Speech error handler пустой**
- `speechRec.onerror = () => {}` -- пользователь не узнает, что микрофон заблокирован или произошла ошибка. Нужен хотя бы toast.

**m-3: Отсутствие aria-live для динамического контента**
- Timeline, Insights, Today Existing -- обновляются динамически, но без `aria-live`. Screen reader не объявит новый контент.
- Исключение: `voiceTranscript` правильно имеет `aria-live="polite"`.

**m-4: Графики (line, bar) не интерактивны**
- AC-9: "все графики интерактивные (тап = детали)". Только heatmap имеет tooltip.

**m-5: Light theme CSS неполный**
- `[data-theme="light"]` CSS НЕ определён в стилях. Есть только `[data-theme="dark"]` и `:root:not([data-theme])`. При выборе "Светлая" тема -- `data-theme="light"` установится, но никакой CSS-селектор его не обрабатывает. Результат: в light-режиме будут те же warm-цвета (fallback на :root).
- Design.md определяет light theme: `--bg-primary: #FAFAFA, --text-primary: #1A1A1A`. Эти значения не реализованы в CSS.

**m-6: Кнопка "Очистить все данные" без undo**
- Используется `confirm()` дважды -- хорошо. Но `localStorage.clear()` удаляет ВСЁ, включая данные других приложений на том же домене. Нужно удалять только ключи с префиксом `wl_`.

**m-7: Tab-навигация -- нет roving tabindex**
- Tab bar использует `role="tablist"` и `role="tab"`, но нет `tabindex="-1"` на неактивных табах. По ARIA best practices, только активный таб должен иметь `tabindex="0"`, остальные `tabindex="-1"`. Стрелки работают (реализовано через keydown), но Tab-ключ не пропускает неактивные табы.

**m-8: textContent для greeting включает escapeHtml вызов**
- Строка 1319: `escapeHtml(name)` внутри `textContent` -- двойная защита. `textContent` сам экранирует, `escapeHtml` избыточен. Не баг, но если имя содержит `&`, отобразится `&amp;` в UI.

**m-9: Heatmap tooltip позиционирование на мобильных**
- Tooltip использует `getBoundingClientRect()` + fixed positioning. На мобильных устройствах при скролле tooltip может оказаться за пределами viewport. Нет clamp-логики.

---

## Accessibility

### Что сделано хорошо

1. `role="tablist"`, `role="tab"`, `role="tabpanel"` -- базовая ARIA-структура навигации
2. `aria-label` на кнопках (микрофон, настройки, закрыть, streak badge)
3. `aria-checked` на category pills
4. `aria-pressed` на filter pills и period switcher
5. `aria-controls` связывает табы с панелями
6. `aria-hidden="true"` на декоративных иконках (onboarding emoji, flame)
7. `aria-live="polite"` на voice transcript
8. `role="dialog"` на onboarding и export modal
9. Keyboard: Arrow Left/Right для переключения табов
10. Keyboard: Escape для закрытия модалок/overlay

### Что отсутствует

1. **Focus trap** в модалках (M-5) -- критично для accessibility
2. **Roving tabindex** в tab bar (m-7)
3. **Skip to main content** link -- отсутствует
4. **aria-live** на динамически обновляемых регионах (m-3)
5. **Focus management** при открытии/закрытии модалок -- фокус не возвращается на триггер-элемент при закрытии
6. **Visible focus indicators** -- нет custom `:focus-visible` стилей. Браузерный outline может быть незаметен на warm-фоне
7. **SVG charts** без текстовой альтернативы кроме `aria-label` на svg. Данные графиков недоступны для screen reader (нет `<desc>` или скрытой таблицы)
8. **Language attribute** -- `lang="ru"` на html-элементе -- ЕСТЬ, хорошо

### WCAG AA контраст -- проверка

| Элемент | Foreground | Background | Ratio | Verdict |
|---------|-----------|------------|-------|---------|
| Body text (warm) | #3D2C1E | #FFF9F0 | ~12.2:1 | PASS |
| Secondary text (warm) | #7A6555 | #FFF9F0 | ~5.1:1 | PASS |
| Muted text (warm) | #B09A88 | #FFF9F0 | ~2.7:1 | **FAIL** (AA requires 4.5:1 for normal, 3:1 for large) |
| Placeholder text | #B09A88 | #FFF3E0 | ~2.5:1 | **FAIL** |
| Text on accent btn | #FFFFFF | #E8A817 | ~2.5:1 | **FAIL** (AA requires 4.5:1) |
| Dark: body text | #F0E8DD | #1C1714 | ~11.5:1 | PASS |
| Dark: secondary text | #B09A88 | #1C1714 | ~4.8:1 | PASS |
| Dark: muted text | #7A6555 | #1C1714 | ~2.6:1 | **FAIL** |
| Dark: text on accent | #FFFFFF | #F5C842 | ~1.8:1 | **FAIL** |
| Tag "career" | #4A90D9 | #EBF3FB | ~3.7:1 | FAIL for small text |
| Tag "health" | #5CB85C | #EDF7ED | ~2.8:1 | **FAIL** |
| Tag "finance" | #2AABB3 | #E6F6F7 | ~3.1:1 | **FAIL** |

**Итого:** 6 из 12 проверенных комбинаций НЕ проходят WCAG AA. Самый критичный -- белый текст на золотой кнопке (основная CTA "Сохранить").

---

## Performance

### Положительное

1. **Нет внешних зависимостей** (без Chart.js, без Dexie.js, без jsPDF) -- SVG-графики самописные, IndexedDB напрямую. Bundle = 1 файл ~92KB.
2. **Пагинация Timeline** -- 20 записей за раз (`TIMELINE_PAGE = 20`), "Загрузить ещё".
3. **Debounce на поиске** -- 300ms, корректно.
4. **Нет утечек памяти** в основном flow -- sparkle-контейнер удаляется через `setTimeout`.

### Потенциальные проблемы

1. **`db.getAll()` вызывается на КАЖДОМ переключении таба** -- при 1000+ записях это может тормозить. Нет кэширования.
2. **Timeline с 1000 записями:** пагинация помогает для DOM, но фильтрация и сортировка происходит на всём массиве (`entries.sort(...)`, `entries.filter(...)`). При 10000 записей это заметно.
3. **Heatmap перерисовывается полностью** при каждом обновлении Insights, включая создание DOM-элементов и привязку event listeners.
4. **Google Fonts** загружается без `font-display: swap` (указан `display=swap` в URL -- проверка: да, `display=swap` в URL Google Fonts -- PASS).
5. **Отсутствие virtual scrolling** для Timeline -- при загрузке 500+ записей все DOM-элементы остаются в памяти.

---

## Security

### Положительное

1. **`escapeHtml()` реализован и применяется** -- через `div.textContent`/`.innerHTML` паттерн. Применяется в:
   - `highlightText()` -- экранирует и текст, и запрос
   - `showMilestone()` -- экранирует текст milestone
   - `refreshInsights()` -- экранирует cat.label, bestWin
   - PDF export -- экранирует текст
2. **`textContent` используется по умолчанию** для вставки пользовательских данных (today existing, timeline cards без поиска)
3. **Нет внешних API-вызовов** -- zero data leaks (кроме Google Fonts)
4. **Нет eval(), нет innerHTML с raw user input**

### Замечания

1. **Google Fonts** -- единственный внешний ресурс. В privacy-first приложении это потенциально трекинг. Рекомендация: self-host шрифт или использовать system fonts.
2. **`localStorage.clear()`** в "Очистить все данные" (m-6) -- удаляет данные всех приложений на домене.
3. **`window.open('', '_blank')`** для PDF -- может быть заблокирован pop-up blocker. Нет обработки этого случая (проверка `if (w)` -- есть, но нет уведомления пользователя при блокировке).

---

## Edge Cases

### 0 записей -- что показывает Insights?

- **Проверено:** `totalWins < 3` показывает прогресс-бар "Ты уже записал(а) 0 из 10". **Корректно.** Не ломается, не показывает пустые графики.
- Timeline: показывает "Здесь будет хронология твоих побед. Начни с первой записи!" **Корректно.**
- Streak: badge скрыт. **Корректно.**

### 1 запись -- Insights?

- `totalWins < 3` -- покажет прогресс "1 из 10". **Корректно.**

### 3 записи -- Insights?

- Insights отображаются, включая Superpower, Line chart, Bar chart, Heatmap. **Корректно.** `totalWins < 3` -- порог, начиная с 3 -- работает.

### 1000 записей -- performance Timeline?

- `db.getAll()` загрузит все 1000 записей в память. `sort()` и `filter()` -- O(n log n) и O(n). Пагинация DOM -- 20 элементов за раз.
- **Риск:** при 10000+ записей `getAll()` может занять 50-100ms на слабых устройствах. Нет индексированного запроса с пагинацией на уровне IndexedDB.
- **Вердикт:** для целевых 1000 записей (~1 год использования) -- приемлемо. Для 5000+ -- нужна оптимизация.

### Очень длинный текст (500+ символов)?

- `max-height: 120px` на `.win-input` + `overflow-y: auto` -- поле ввода скроллится. **Корректно.**
- В Timeline: текст выводится полностью через `li.textContent`. Нет `text-overflow: ellipsis` или truncation. Карточка растянется вертикально.
- **Minor risk:** на 320px viewport карточка с 500-символьным текстом займёт значительную часть экрана, но не сломает layout.

### Спецсимволы (<script>, HTML tags)?

- **Проверено:** `textContent` используется при обычном рендере. `escapeHtml` при search-highlight. **Безопасно.**
- Тест: запись `<script>alert('xss')</script>` -- отобразится как текст. **PASS.**

### Одновременно 2 голосовых ввода?

- **Невозможно by design:** один `speechRec` объект, одна `activeVoiceField`. Voice overlay блокирует UI (fullscreen overlay с z-index: 180). Второй голосовой ввод невозможно запустить. **PASS.**

### IndexedDB quota exceeded?

- `saveEntry` содержит `try/catch` с fallback на FallbackDB (строка 1176-1181). **Корректно.**
- Однако: `FallbackDB._write` тоже обёрнут в `try/catch {}` с пустым catch (строка 907). Если и localStorage переполнен -- данные молча теряются. Нет уведомления пользователю.
- **Major risk:** потеря данных без уведомления. Нужен toast/alert при ошибке сохранения.

### Safari: Web Speech API?

- `SpeechAvailable` проверяется корректно. Safari не поддерживает SpeechRecognition -- кнопки микрофона будут скрыты. **PASS.**

### prefers-color-scheme: dark + manual theme toggle?

- CSS: `:root:not([data-theme="warm"]):not([data-theme="light"])` -- авто-dark применяется только если нет manual theme.
- При выборе "Тёплая" -- `data-theme` удаляется (`removeAttribute`), и авто-dark из `prefers-color-scheme` сработает.
- **Bug:** Если пользователь выбрал "Тёплая" тему, но его OS в dark mode -- CSS медиа-запрос для dark ПРИМЕНИТСЯ (т.к. нет `data-theme` атрибута). Тёплая тема ПЕРЕЗАПИШЕТСЯ тёмной через `prefers-color-scheme: dark`.
- **Воспроизведение:** Settings > "Тёплая" > OS Dark Mode = пользователь получит тёмную тему вместо тёплой.
- **Severity:** Major (M-6). Нарушает ожидания пользователя.

---

## Дополнительные находки

### Streak edge case

- Если пользователь удалит все записи за сегодня через кнопки "x" в "Сегодняшние записи" -- streak не пересчитается до следующего `refreshToday()`. Стоит вызывать `checkStreak()` после удаления.

### Export preview не обновляется при смене формата

- При переключении с TXT на PDF -- preview остаётся текстовым. Для PDF нет preview (и нет реального PDF).

### Delete win button -- splice index bug

- Строка 1261: `entry.wins.splice(wi, 1)` -- `wi` берётся из замыкания `forEach`. Если пользователь удаляет записи последовательно (не обновляя список), индексы сдвигаются. Однако `refreshTodayExisting()` вызывается после каждого удаления (строка 1267), пересоздавая DOM. **Не баг, т.к. DOM обновляется.** Но если два быстрых клика -- возможна гонка на async.

### Onboarding не доступен повторно

- Нет кнопки "Пройти onboarding снова" в настройках. Единственный способ -- "Очистить все данные". Не баг, но UX concern.

---

## Сводная таблица багов

| ID | Severity | Описание | Файл:строка |
|----|----------|----------|-------------|
| C-1 | Critical | Нет Service Worker, Push Notifications, manifest.json | index.html (отсутствует) |
| C-2 | Critical | Нет Pie Chart (AC-7 explicit requirement) | index.html:1603 |
| M-1 | Major | Calendar view -- нет тапа на день = список побед | index.html:1768 |
| M-2 | Major | PDF export через window.print(), не реальный PDF | index.html:1893 |
| M-3 | Major | Нет Sunday Review, нет тренда vs прошлая неделя | index.html:1581 |
| M-4 | Major | Поиск не работает по дате | index.html:1479 |
| M-5 | Major | Focus trap отсутствует во всех модалках | index.html:769,790,664 |
| M-6 | Major | Warm theme + OS dark mode = конфликт CSS | index.html:57-71 |
| m-1 | Minor | Onboarding step 1 не валидирует пустое имя (UX) | index.html:1021 |
| m-2 | Minor | Speech error handler пустой | index.html:1359 |
| m-3 | Minor | Нет aria-live на динамических регионах | index.html (множество) |
| m-4 | Minor | Графики line/bar не интерактивны | index.html:1674,1731 |
| m-5 | Minor | Light theme CSS не реализован | index.html:57 |
| m-6 | Minor | localStorage.clear() вместо selective delete | index.html:1997 |
| m-7 | Minor | Tab bar -- нет roving tabindex | index.html:752 |
| m-8 | Minor | escapeHtml внутри textContent = двойное экранирование | index.html:1319 |
| m-9 | Minor | Heatmap tooltip без viewport clamp | index.html:1819 |
| m-10 | Minor | Quota exceeded -- молчаливая потеря данных | index.html:907 |
| m-11 | Minor | WCAG AA: 6 из 12 цветовых комбинаций FAIL | index.html:16-83 |

---

## Рекомендации (приоритизированные)

### P0 -- Blockers для релиза

1. **Добавить Service Worker + manifest.json** -- без этого app не PWA, не installable, не offline.
2. **Исправить WCAG AA контраст** -- особенно белый текст на золотой кнопке (#FFFFFF на #E8A817, ratio 2.5:1). Решение: затемнить кнопку до ~#996D0D или использовать тёмный текст.
3. **Исправить конфликт warm theme + prefers-color-scheme: dark** -- добавить `[data-theme="warm"]` селектор в CSS, или при выборе warm явно ставить `data-theme="warm"`.

### P1 -- Обязательные для AC compliance

4. **Реализовать Pie Chart** для AC-7 -- SVG pie chart аналогично текущим SVG-графикам. ~50 строк кода.
5. **Calendar view с кликом на день** -- AC-4 требует список побед при тапе. Можно расширить heatmap или добавить секцию в Insights.
6. **PDF экспорт через jsPDF или html2canvas** -- или хотя бы честно переименовать в "Печать".
7. **Sunday Review** -- добавить карточку-баннер при входе в воскресенье + тренд vs прошлая неделя.
8. **Поиск по дате** -- добавить проверку по `e.date` в фильтре Timeline.
9. **Light theme CSS** -- добавить `[data-theme="light"]` блок с нейтральными цветами из design.md.

### P2 -- Accessibility

10. **Focus trap** в модалках -- `inert` attribute на фон или manual trap.
11. **Focus management** -- при открытии модалки фокус на первый интерактивный элемент, при закрытии -- возврат на триггер.
12. **Roving tabindex** в tab bar.
13. **aria-live** на Timeline list, Insights cards, Today existing.
14. **Visible focus-visible styles** -- custom outline для warm/dark themes.
15. **Скрытая таблица данных** рядом с SVG-графиками для screen readers.

### P3 -- Polish

16. **Toast/notification при ошибке сохранения** вместо silent catch.
17. **Selective localStorage cleanup** (только `wl_*` ключи).
18. **Self-host Inter font** или fallback на system fonts для privacy.
19. **Streak пересчёт после удаления записей.**
20. **Speech error feedback** -- toast "Микрофон не доступен".

---

## Вердикт

Код написан аккуратно и с пониманием UX. HTML-структура семантична, ARIA-атрибуты на месте для основных компонентов, XSS-защита реализована грамотно. Самописные SVG-графики -- хорошее решение вместо тяжёлых библиотек. IndexedDB-обёртка с localStorage fallback -- правильный подход.

Однако:
- **2 Critical бага** (нет PWA-инфраструктуры, нет pie chart)
- **6 Major багов** (calendar tap, PDF, Sunday Review, search, focus trap, theme conflict)
- **11 Minor багов**
- **6 из 12 цветовых комбинаций не проходят WCAG AA**
- **4 из 12 AC имеют неполную реализацию** (AC-4, AC-7, AC-8, AC-10)

**Текущая оценка: 7.2/10**

После фикса P0 + P1 (пункты 1-9): прогноз **9.0+/10**.
После фикса P0 + P1 + P2 (пункты 1-15): прогноз **9.5/10**.
