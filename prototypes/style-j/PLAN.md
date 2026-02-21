# Style J: Research Analytics Dashboard — Design Plan

## 1. Design Philosophy

**Inspiration**: Elsevier SciVal meets Stripe Dashboard — data-dense yet breathable.

The Research Analytics Dashboard prioritizes **clarity of quantitative data** within an academic context. Every pixel serves the goal of helping researchers and administrators understand research output, funding status, and collaboration networks at a glance. The design feels institutional yet modern — conveying authority through clean typography and structured layouts rather than decorative elements.

Key principles:
- **Data-first**: Numbers, charts, and metrics are the heroes — not chrome or decoration
- **Progressive disclosure**: Overview first, details on demand
- **Purposeful animation**: Motion draws attention to changing data and guides the eye through information hierarchy
- **Academic rigor meets modern UX**: The seriousness of academic reporting combined with the usability of modern SaaS dashboards

## 2. Color System

### Primary Palette
| Token | Hex | Usage |
|-------|-----|-------|
| `slate-800` | `#1e293b` | Sidebar background |
| `slate-700` | `#334155` | Sidebar hover states |
| `slate-600` | `#475569` | Secondary text |
| `slate-100` | `#f1f5f9` | Page background |
| `white` | `#ffffff` | Card backgrounds |

### Accent Colors
| Token | Hex | Usage |
|-------|-----|-------|
| `indigo-600` | `#4f46e5` | Primary accent — links, active states, primary buttons |
| `indigo-50` | `#eef2ff` | Light accent backgrounds |
| `emerald-500` | `#10b981` | Positive metrics, completed status, growth indicators |
| `emerald-50` | `#ecfdf5` | Positive metric backgrounds |
| `amber-500` | `#f59e0b` | Warnings, pending status, deadlines approaching |
| `amber-50` | `#fffbeb` | Warning backgrounds |
| `rose-500` | `#f43f5e` | Negative metrics, overdue, declined |
| `rose-50` | `#fff1f2` | Negative backgrounds |

### Chart Colors (ordered for visual distinction)
1. `indigo-500` (#6366f1) — Mobilities
2. `emerald-500` (#10b981) — Knowledges
3. `amber-500` (#f59e0b) — Moralities
4. `rose-500` (#f43f5e) — Learning
5. `violet-500` (#8b5cf6) — Aesthetics

## 3. Typography

**Font**: Inter (Google Fonts) — designed for screen readability, excellent at small sizes for data-heavy UIs.

| Element | Weight | Size | Tracking |
|---------|--------|------|----------|
| Page title | 700 (bold) | text-2xl (24px) | normal |
| Section heading | 600 (semibold) | text-lg (18px) | normal |
| Card title | 500 (medium) | text-sm (14px) | wide (tracking-wide, uppercase) |
| KPI number | 700 (bold) | text-3xl (30px) | tight |
| Body text | 400 (regular) | text-sm (14px) | normal |
| Caption/meta | 400 (regular) | text-xs (12px) | normal |
| Sidebar nav | 500 (medium) | text-sm (14px) | normal |
| Sidebar sub-nav | 400 (regular) | text-xs (12px) | normal |

Monospace for data: `font-mono` for numbers in tables and KPIs to maintain column alignment.

## 4. Navigation Pattern

**Left sidebar (w-56, 224px)** — fixed position, full height, slate-800 background.

### Structure (top to bottom):
1. **Logo area**: "AMCA" wordmark + "Research Analytics" subtitle (text-xs, slate-400)
2. **Search bar**: Compact search input (Cmd+K hint), slate-700 background, rounded
3. **Primary nav group** — "Overview":
   - Dashboard (grid icon) — `/dashboard.html`
4. **Secondary nav group** — "Research":
   - Persons (users icon) — `/listing.html` — shortcut hint: `P`
   - Projects (folder icon) — `/projects.html` — shortcut hint: `R`
   - Events (calendar icon) — `/events.html` — shortcut hint: `E`
   - Institutions (building icon) — `/institutions.html` — shortcut hint: `I`
5. **Tertiary nav group** — "System":
   - Back to Prototypes (arrow-left icon) — `../index.html`

### Behavior:
- Active page: indigo-500 left border (3px), white text, indigo-900/20 background
- Hover: slate-700 background, smooth transition
- Mobile: hamburger button at top-left, sidebar slides in as overlay with backdrop blur
- Keyboard shortcuts: indicated as subtle kbd badges on the right side of nav items

## 5. Animation Strategy

### On-Load Animations (purpose: orient the user)
- **KPI counters**: Count up from 0 using JS `requestAnimationFrame` over 1.5s with easeOutExpo curve
- **Cards**: Staggered fadeIn + translateY(10px) — 0ms, 80ms, 160ms, 240ms delays
- **Sidebar**: slideIn from left (200ms) — only on first load
- **Progress bars**: Animate width from 0 to target over 1s with easeOutCubic

### Interaction Animations (purpose: provide feedback)
- **Card hover**: translateY(-2px) + subtle shadow increase (150ms ease)
- **Button hover**: scale(1.02) + background color shift (100ms)
- **Row hover in tables**: background color shift to indigo-50 (100ms)
- **Active/click states**: scale(0.98) briefly (50ms) then return

### Scroll Animations (purpose: reveal content progressively)
- **Timeline nodes**: scaleIn from center as they enter viewport (IntersectionObserver)
- **Chart bars**: Grow from bottom on scroll into view

### Transition Animations (purpose: smooth state changes)
- **Filter changes**: Rows fade out/in with 200ms transition
- **Tab switches**: Content area crossfade (150ms)

### NOT animated (restraint is key):
- Navigation — immediate response, no delays
- Text content — readable immediately, never animated
- Data in tables — appears instantly for scanability

## 6. Per-Page Wireframe Descriptions

### Page 1: dashboard.html — Research Overview

```
+--sidebar--+--main content area (p-8)----------------------------+
|            | Page title: "Research Overview"     [date range]    |
|  AMCA      |                                                     |
|  [search]  | ROW 1: KPI Cards (4 columns, gap-6)                |
|            | [Researchers: 18] [Projects: 12] [Events: 12] [Pub:|
|  Dashboard | [+3 this year   ] [6 active   ] [4 upcoming] [42  ]|
|  --------  | [sparkline      ] [sparkline  ] [sparkline ] [spar]|
|  Persons   |                                                     |
|  Projects  | ROW 2: Two columns (7/5 split)                      |
|  Events    | LEFT: Research Output by Section (stacked bar chart)|
|  Institut. |   - 5 sections, bars animated on load               |
|            |   - Legend below chart                               |
|  --------  | RIGHT: Grant Progress                                |
|  <- Proto  |   - 4 grants with animated progress bars            |
|            |   - Amount funded / total                            |
|            |                                                      |
|            | ROW 3: Two columns (1/1 split)                       |
|            | LEFT: Upcoming Deadlines                             |
|            |   - 5 items with countdown badges                   |
|            |   - Color-coded urgency                              |
|            | RIGHT: Recent Activity Feed                          |
|            |   - 8 items, timeline-style with dots                |
|            |   - Staggered reveal animation                       |
+------------+-----------------------------------------------------+
```

### Page 2: listing.html — Persons

```
+--sidebar--+--main content area----------------------------------+
|            | "Researchers"                     [Add Person btn]  |
|            |                                                     |
|            | Filter Bar: [Search...] [Section ▼] [Status ▼]     |
|            |             [Sort: Name | Publications | h-index]   |
|            |                                                     |
|            | Summary: "18 researchers across 5 sections"          |
|            |                                                     |
|            | TABLE (full width, card-style with rounded corners) |
|            | TH: Name | Institution | Section | Pubs | h-index  |
|            | --------------------------------------------------------|
|            | [AO] Dr. Amina Osei  | U Ghana | Mob | 12 |▁▂▃▅| 8 |
|            | [KA] Prof. K. Asante | UCT     | Kno | 24 |▂▃▅▇| 14|
|            | [FD] Dr. F. Diallo   | UCAD    | Mor |  9 |▁▂▃▄| 6 |
|            | ... (12 total rows, staggered reveal)                |
|            |                                                      |
|            | Pagination: < 1 2 >                                  |
+------------+-----------------------------------------------------+
```

Each row has:
- Initials avatar (indigo background, white text)
- Name as link to detail.html
- Institution
- Research section with colored dot
- Publication count (mono font)
- Inline sparkline SVG (last 5 years of publications)
- h-index (mono font)
- Row animates in with slideIn, staggered 50ms per row

### Page 3: detail.html — Person Profile (Dr. Amina Osei)

```
+--sidebar--+--main content area----------------------------------+
|            | Breadcrumb: Researchers > Dr. Amina Osei            |
|            |                                                     |
|            | HEADER CARD (full width)                             |
|            | [AO avatar 64px] Dr. Amina Osei                     |
|            |                  Senior Research Fellow              |
|            |                  University of Ghana | Mobilities    |
|            |                  [email] [ORCID link]                |
|            |                                                      |
|            | METRICS ROW (4 cards)                                |
|            | [Publications: 12] [Citations: 89] [h-index: 8]     |
|            | [Projects: 3]                                        |
|            | (each with animated counter)                         |
|            |                                                      |
|            | TWO COLUMNS (7/5)                                    |
|            | LEFT: Publication Timeline                           |
|            |   - Bar chart (CSS) by year (2019-2024)             |
|            |   - Animated bars growing up                         |
|            |                                                      |
|            | RIGHT: Research Focus                                |
|            |   - Horizontal bar chart: topic areas                |
|            |   - Mobility, Migration, Diaspora Studies, etc.      |
|            |                                                      |
|            | FULL WIDTH: Projects (3 cards)                       |
|            |   - Project name, role, dates, progress bar          |
|            |                                                      |
|            | FULL WIDTH: Events (timeline, 5 items)               |
|            |                                                      |
|            | FULL WIDTH: Publications List (4 items)              |
|            |   - Title, journal, year, citation count             |
|            |                                                      |
|            | FULL WIDTH: Fellowships (2 items)                    |
+------------+-----------------------------------------------------+
```

### Page 4: projects.html — Research Projects

```
+--sidebar--+--main content area----------------------------------+
|            | "Research Projects"               [New Project btn]  |
|            |                                                      |
|            | Filter: [All] [Active] [Planned] [Completed]         |
|            | Summary: "12 projects | EUR 2.4M total funding"      |
|            |                                                      |
|            | GANTT TIMELINE (full width card)                      |
|            | Y-axis: Project names (12)                            |
|            | X-axis: 2020 — 2027 (year markers)                    |
|            | Bars colored by section, animated width               |
|            | Milestone diamonds on bars                            |
|            | Hover: tooltip with details                           |
|            |                                                       |
|            | TWO COLUMNS (1/1)                                     |
|            | LEFT: Funding by Section (donut-style ring chart)     |
|            |   - CSS conic-gradient, animated rotation             |
|            |   - Legend with amounts                               |
|            |                                                       |
|            | RIGHT: Project Status Breakdown                       |
|            |   - 3 status cards: Active(6), Planned(3), Done(3)   |
|            |   - Each with mini list of project names              |
|            |                                                       |
|            | FULL WIDTH: Project Cards Grid (3 columns)            |
|            |   - 12 cards with: title, PI, dates, funding,        |
|            |     progress bar, section badge                       |
|            |   - Staggered scaleIn animation                      |
+------------+------------------------------------------------------+
```

### Page 5: events.html — Events

```
+--sidebar--+--main content area----------------------------------+
|            | "Events"                           [Add Event btn]   |
|            |                                                      |
|            | Toggle: [Upcoming] [Past] [All]                       |
|            |                                                      |
|            | COUNTDOWN CARDS (3 columns, upcoming only)            |
|            | Next 3 events with:                                   |
|            |   - Event name, type badge, date                      |
|            |   - Countdown: DD:HH:MM (animated digits)             |
|            |   - Location                                          |
|            |                                                       |
|            | CALENDAR HEATMAP (full width card)                    |
|            |   - 12 months x ~30 days grid (like GitHub)           |
|            |   - Color intensity = number of events                |
|            |   - Month labels on top                               |
|            |   - Animated cell reveals                             |
|            |                                                       |
|            | TIMELINE (full width)                                 |
|            |   - Vertical timeline with alternating left/right     |
|            |   - 12 events with date, title, type, location        |
|            |   - Animated node reveals on scroll                   |
|            |   - Type icons: conference, workshop, lecture, seminar |
+------------+------------------------------------------------------+
```

### Page 6: institutions.html — Partner Network

```
+--sidebar--+--main content area----------------------------------+
|            | "Partner Institutions"                                |
|            |                                                      |
|            | Summary: "14 institutions | 8 countries | 2 cont."   |
|            |                                                      |
|            | GEOGRAPHIC GROUPS (2 sections)                        |
|            |                                                      |
|            | "African Partners" heading                            |
|            | TABLE:                                                |
|            | Name | Country | Members | Projects | Collab Score   |
|            | [bar chart for members] [bar for projects]            |
|            | U of Ghana | Ghana | ████ 4 | ███ 3 | ●●●●○         |
|            | UCT        | SA    | ██ 2   | ████ 4 | ●●●○○         |
|            | ... 6 African institutions                            |
|            |                                                      |
|            | "European Partners" heading                           |
|            | TABLE: (same format)                                  |
|            | U Bayreuth | Germany | ██████ 8 | █████ 6 | ●●●●● |
|            | ... 6 European institutions                           |
|            |                                                      |
|            | COLLABORATION MATRIX (full width card)                |
|            |   - Heatmap grid: institution x institution           |
|            |   - Color intensity = joint projects                  |
|            |   - Animated cell reveals                             |
+------------+------------------------------------------------------+
```

## 7. UX Principles

1. **Scanability**: The most important number on every page is the largest. Secondary information uses smaller type or muted colors.
2. **Keyboard-first navigation**: Cmd+K for search, P/R/E/I for pages, Esc to close modals.
3. **Consistent card anatomy**: Every card follows: Label (uppercase, xs, muted) > Value (bold, lg) > Context (xs, trend indicator).
4. **Color as data**: Colors always mean something — emerald=positive, amber=caution, rose=negative, indigo=neutral/active. Never decorative.
5. **Responsive without loss**: Mobile stacks columns but never hides data. Tables become cards on mobile.
6. **Immediate feedback**: All interactive elements respond within 100ms. No loading states for static data.
7. **Breadcrumb navigation**: Detail pages always show path back to listing.
8. **Persistent context**: Sidebar shows current page, filters persist across navigation (via URL params in real app).

## 8. Unique Features

1. **Animated KPI counters**: Numbers physically count up from 0 on page load — makes data feel alive and draws attention
2. **Inline SVG sparklines**: Tiny trend charts embedded in table cells — shows trajectory without leaving context
3. **CSS-only Gantt chart**: Project timelines rendered purely with CSS grid and animated bars — no chart library needed
4. **GitHub-style calendar heatmap**: Event density visualization using CSS grid — immediately shows busy periods
5. **Countdown timers**: Live-updating countdowns for upcoming deadlines/events — creates urgency
6. **Collaboration strength matrix**: Heatmap showing institution-to-institution cooperation intensity
7. **Progress bar animations**: Grant and project progress bars fill smoothly on load — satisfying visual feedback
8. **Staggered card reveals**: Cards appear one after another with precise timing — guides the eye through content hierarchy
9. **Keyboard shortcut hints**: Navigation items show keyboard shortcuts — power users can navigate without mouse
10. **Section-coded color system**: Each research section has a consistent color across all charts and badges — builds recognition
