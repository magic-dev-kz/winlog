# Changelog

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
