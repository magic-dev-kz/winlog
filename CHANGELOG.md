# Changelog

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
