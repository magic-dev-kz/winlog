# Changelog



## v26.0 (2026-03-29) — Deferred Init for Faster First Paint

- **Performance: deferred non-critical init**: Reminder setup and SW registration wrapped in `requestIdleCallback` (with `setTimeout` fallback) so main UI renders before secondary features load
- SW cache bumped to `winlog-v26.0`

---
## v25.0 (2026-03-29) — Security Meta Tags

- **Security hardening**: Added `X-Content-Type-Options: nosniff`, `referrer: no-referrer`, and `format-detection: telephone=no` meta tags to `<head>`
- SW cache bumped to `winlog-v25.0`

---
## v24.0 (2026-03-29) — JSON-LD Structured Data

- **JSON-LD structured data**: Added WebApplication schema markup in `<head>` for improved SEO and rich search results
- SW cache bumped to `winlog-v24.0`

---
## v23.0 (2026-03-29) — Deferred Font Loading

- **Non-blocking Google Fonts**: Font CSS changed from render-blocking `<link rel="stylesheet">` to `<link rel="preload" ... onload>` with `<noscript>` fallback — improves First Contentful Paint
- SW cache bumped to `winlog-v23.0`

---
## v22.0 (2026-03-29) — JSON Backup/Restore

- **JSON backup/restore**: Export button in Settings downloads full journal as JSON (all entries, mood, gratitude, categories, settings). Import button merges data — deduplicates by date+content, preserves existing entries, restores missing settings
- SW cache bumped to `winlog-v22.0`

## v21.0 (2026-03-29) — Entry Templates

- **Entry templates**: Three template buttons above win fields — "Quick win", "Achievement", "Milestone" — each pre-fills empty win inputs with Russian-language prompts (e.g., "Быстрая победа:", "Достижение дня:", "Веха:"); only fills empty fields; visual feedback on click; auto-focuses first input
- SW cache bumped to `winlog-v21.0`

## v20.0 (2026-03-29) — Print Styles

- **Print stylesheet**: `@media print` rules — hides onboarding, settings, tab bar, modals, voice overlay; shows today's wins + timeline entries; white bg, black text; page breaks on timeline cards
- SW cache bumped to `winlog-v20.0`

## v19.0 (2026-03-29) — Error Handling Hardening

- **Empty entry guard**: Prevent saving when all fields are empty — shows toast + shake animation
- SW cache bumped to `winlog-v19.0`

## v18.0 (2026-03-29) — SEO / Meta Pass

- **robots meta**: Added `<meta name="robots" content="index, follow">`
- **apple-touch-icon**: Inline SVG data URL with product emoji (🏆)
- SW cache bumped to `winlog-v18.0`

## v17.0 (2026-03-29) — Accessibility Pass

- **Skip link**: Already present (verified)
- **Win textarea**: Already had `aria-label` per entry (verified)
- **Mood buttons**: Changed from `role="radio"` + `aria-checked` to `aria-pressed` toggle buttons; mood row changed from `radiogroup` to `group`
- SW cache bumped to `winlog-v17.0`

## v16.0 (2026-03-29) — Entry Character Count

- **Character Count**: Shows character count on each win entry textarea, with "detailed win!" badge at 200+ characters
- SW cache bumped to `winlog-v16.0`
## v15.0 — Random Reflection Prompt (2026-03-29)

**Random Reflection Prompt**
- New "Reflect" card in Insights tab with a daily-changing prompt
- 15 reflection prompts about patterns, growth, consistency, and self-awareness
- Prompt selected by day-of-year modulo, changes every day
- Styled with accent-colored left border and italic text
- "New prompt every day" caption below the prompt
- Placed after Monthly Highlights card in the insights flow

### Technical
- Service worker cache bumped to `winlog-v15.0`

---

## v14.0 — Win Streak Freeze (2026-03-29)

**Win Streak Freeze**
- 1 streak freeze per month for streak protection
- Snowflake button appears next to the streak badge when a freeze is available
- Using a freeze marks the previous day as "frozen" so the streak doesn't break
- `calculateStreak` now treats frozen dates as valid streak days
- Freeze state persisted in localStorage (`wl_streak_freezes`) keyed by year-month
- Button shows "Used" state when monthly freeze is spent
- Service worker cache bumped to `winlog-v14.0`

---

## v13.0 — Monthly Highlights (2026-03-29)
- **Monthly Highlights card** in Insights: "Best Day: March 15 (5 wins)", "Most Active Category: Work (42%)", "Longest Streak: 12 days"
- Three highlight rows with icons (trophy, chart, fire) on accent background
- Calculates from current month's entries; hidden if fewer than 2 entries
- Service worker cache bumped to `winlog-v13.0`

---

## v12.0 — Zoom, Sparkline & Sound (2026-03-29)
- **Entry Word Count**: live word counter shown below win fields while typing; auto-hides when empty
- **Mood Trend Sparkline**: small bar chart in the mood section showing mood distribution over the last 30 days with colored bars and legend; updates on save
- **Save Sound**: soft ascending two-tone chime (C5-E5 + G5 shimmer) via Web Audio API plays on successful save
- Service worker cache bumped to `winlog-v12.0`

---

## v11.0 — Micro-polish (2026-03-29)
- Onboarding: confetti burst on "Start Winning" CTA click (24 colored particles)
- Save button: green success flash animation on save (`saveFlash` keyframe)
- Service worker cache bumped to `winlog-v11.0`

---

## v10.0 — Micro-polish (2026-03-29)
- Gratitude field placeholder updated to "What are you grateful for today?"
- Save button hover glow stronger for better visual feedback
- Service worker cache bumped to `winlog-v10.0`

---

## v9.0 — Share on X & Search Highlight (2026-03-29)
- **Share on X**: Button below Share Achievement Card. Pre-filled tweet: "X wins recorded this month. Track yours: [URL]"
- **Timeline Search Highlight**: Search matches highlighted with yellow `<mark>` tags (confirmed existing since v3)
- Service worker cache bumped to `winlog-v9.0`

## v8.0 — Gratitude Prompt, Category Pie Chart & Dark Mode (2026-03-29)
- **Gratitude Prompt**: Optional "What are you grateful for?" textarea on the Today screen, between categories and mood. Saved with entry data (`gratitude` field), displayed on timeline cards and today's existing entries with a heart icon
- **Win Categories Stats**: Pie chart in Insights showing distribution of wins across categories with SVG donut chart and legend (already present since v3, confirmed working)
- **Dark Mode Toggle**: Three-way theme switcher (Warm / Light / Dark) in Settings panel with `data-theme` attribute and full CSS custom property overrides (already present since v3, confirmed working)
- Service worker cache bumped to `winlog-v8.0`

## v7.0 — PWA Install, Keyboard Shortcut & Auto-save Draft (2026-03-29)
- **PWA Install Prompt**: `beforeinstallprompt` banner shown after 2+ visits, with Install/Dismiss buttons. Dismissed state persisted in localStorage
- **Keyboard Shortcut**: Ctrl+Enter (or Cmd+Enter on Mac) saves the current win entry
- **Auto-save Draft**: Win textarea content auto-saved to localStorage on every keystroke (`wl_draft`). Draft restored on page load, cleared on successful save
- Service worker cache bumped to `winlog-v7.0`

## v6.0 — Animations & Focus Polish (2026-03-29)
- **Win Save Animation**: Pulse glow on today-existing card + styled "Win recorded!" toast on every save
- **Streak Counter CountUp**: Streak number animates from 0 to current value over 0.8s (easeOutCubic) on first load
- **Focus-Visible**: Comprehensive `:focus-visible` styles for all interactive elements (pills, pin buttons, delete buttons, mic buttons, mood buttons, filter pills, settings gear, period switcher, streak trophies, links, selects)
- **Timeline Card Stagger**: Cards in timeline appear with dynamic staggered delays (50ms per card) instead of fixed nth-child rules, supporting any number of cards
- **SW**: Cache version bumped to v6.0

## v5.0 — Daily Prompt, Growth Chart & Share Card (2026-03-29)
- **Daily Prompt**: Inspirational question of the day shown on the Today screen (32 prompts, rotated by day of year). Encourages reflection: "What are you proud of today?", "What obstacle did you overcome?", etc.
- **Growth Chart**: SVG line chart in Insights showing win counts per week over the last 8 weeks. Includes area gradient fill, per-point labels, and summary stats (total wins, this week, trend vs last week)
- **Share Achievement Card**: Canvas-rendered 600x400 card displaying total wins, current streak, favorite category, and WinLog branding. Web Share API integration for native sharing on supported devices, plus PNG download fallback. Modal with preview
- **SW**: Cache version bumped to v5.0

## v4.0 — Search, Pin, Mood & Streak Achievements (2026-03-29)
- **Search & Filter**: Full-text search across wins, category filter pills, date range filter (this week / this month / all time), search results highlighted with `<mark>`
- **Pin Important Wins**: Pin button on every timeline card, pinned wins shown at top of timeline with golden accent, max 5 pinned wins, persisted in localStorage
- **Mood Tracker**: Optional emoji mood selector (5 moods) on the Today screen, mood saved with entries, mood displayed inline on timeline cards, mood distribution bar chart in Insights, weekly mood summary stat
- **Streak Achievements**: Milestone trophies (7, 14, 21, 30, 60, 90 days) displayed in header, locked/unlocked states with grayscale, congratulations overlay with confetti animation on milestone achievement, milestones persisted in localStorage
- **SW**: Cache version bumped to v4.0

## v3.0 — Premium Visual Redesign (2026-03-29)
- **Gradients**: Multi-layered radial gradients on body background with warm ambient tones
- **Micro-animations**: Spring-curve `cardIn` keyframes for card/entry entrances with staggered delays; shimmer sweep on primary button hover
- **Shadow system**: Dual-layer shadows (ambient + direct) on all cards; `--shadow-card-hover` with accent glow for interactive states
- **Glassmorphism**: `backdrop-filter: blur(20px) saturate(180%)` on tab bar, onboarding card, export modal, settings button, voice overlay
- **Buttons**: Gradient backgrounds on primary actions with animated shimmer `::before` pseudo-element; glow shadow intensifies on hover; spring-curve press feedback
- **Typography**: Weight 800-900 for hero/headings; `letter-spacing: -0.02em`; gradient text (`background-clip`) on greeting, onboarding title, superpower category, milestone number, streak counter
- **Cards/entries**: Spring entrance animation with staggered delays; colored `border-left` on timeline cards; hover lift + glow; win fields animate in sequence
- **Navigation tabs**: Gradient active state text; `translateY(-2px)` float on hover; icon scale 1.15x on hover
- **Input fields**: Focus ring (`box-shadow: 0 0 0 4px` accent) on all inputs; hover border hint color shift
- **Heatmap**: Richer color stops for heatmap levels
- **Streak counter**: Gradient text with pulsing glow animation; badge glows with `glowPulse` keyframes
- **Settings gear**: Glassmorphism background; 30deg rotation on hover
- **Period switcher**: Gradient slider for active period
- **Progress bars**: Gradient fill (accent to amber)
- **Category/filter pills**: Hover lift with subtle shadow

## v1.0 (2026-03-29)
- Initial release
- Ship-ready (9.0/10)
- PWA (service worker + manifest)
- WCAG AA accessible
- Works offline
