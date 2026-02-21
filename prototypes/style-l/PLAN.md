# Style L — Grant Lifecycle Tracker

## Design Philosophy
A funding-focused academic management tool inspired by NIH Reporter meets Monday.com. Every design decision centers on **financial clarity**, **deadline awareness**, and **grant lifecycle visibility**. The interface treats grants as living entities moving through phases, with budgets as the primary lens for understanding project health.

## Color System
| Token | Hex | Usage |
|-------|-----|-------|
| Teal-700 (Primary) | `#0f766e` | Primary actions, active states, sidebar accents |
| Teal-50 | `#f0fdfa` | Active item backgrounds, hover states |
| Teal-100 | `#ccfbf1` | Light accent backgrounds |
| Slate-50 | `#f8fafc` | Page background |
| Slate-100 | `#f1f5f9` | Card backgrounds, table stripes |
| Slate-800 | `#1e293b` | Sidebar background |
| Slate-900 | `#0f172a` | Primary text |
| Emerald-500 | `#10b981` | Funded/approved status, positive trends |
| Emerald-50 | `#ecfdf5` | Success backgrounds |
| Amber-500 | `#f59e0b` | Pending status, warnings, <30 day deadlines |
| Amber-50 | `#fffbeb` | Warning backgrounds |
| Rose-500 | `#f43f5e` | Overdue, negative trends, <7 day deadlines |
| Rose-50 | `#fff1f2` | Danger backgrounds |
| Sky-500 | `#0ea5e9` | ERC funder badge, informational |
| Violet-500 | `#8b5cf6` | EU Horizon funder badge |

## Typography
- **Font**: Inter (Google Fonts), weights 400/500/600/700
- **Headings**: text-2xl font-bold slate-900 for page titles, text-lg font-semibold for section headers
- **Body**: text-sm font-normal slate-600
- **Numbers/Financial**: font-mono or tabular-nums for alignment, font-bold for emphasis
- **Badges**: text-xs font-medium uppercase tracking-wide

## Navigation — Collapsible Left Sidebar
- Width: w-60 expanded, w-16 collapsed
- Background: slate-800, text slate-300
- Logo area at top with cluster icon + "Africa Multiple" text (hidden when collapsed)
- Sections with expandable sub-items:
  - **Overview** (icon: chart-bar): Dashboard
  - **People** (icon: users): Persons, Person Detail
  - **Research** (icon: beaker): Projects
  - **Events** (icon: calendar): Events
  - **Partners** (icon: building): Institutions
- Active item: teal left border (3px), teal-50/10 background, white text
- Hover: slate-700 background
- Collapse toggle button at bottom
- "All Prototypes" link at very bottom

## Animation Strategy
1. **Page Load**: Cards slide up with staggered delays (0.1s increments)
2. **Number Counters**: Animated count-up from 0 to target value over 1.5s using Alpine.js
3. **Donut Charts**: SVG stroke-dashoffset animation from full circumference to target
4. **Progress Bars**: Width animates from 0 to target percentage over 1s
5. **Lifecycle Steppers**: Steps reveal sequentially with scale + opacity (0.15s delay each)
6. **Current Phase Pulse**: Box-shadow pulse animation on the active lifecycle step
7. **Sparklines**: SVG path draws in using stroke-dasharray animation
8. **Trend Arrows**: Fade + slight vertical translate on load
9. **Countdown Timers**: Static display with color-coded urgency (no real-time tick)

## Key CSS Animations
```css
@keyframes fillDonut { from { stroke-dashoffset: var(--circumference); } to { stroke-dashoffset: var(--offset); } }
@keyframes stepReveal { from { opacity: 0; transform: scale(0.5); } to { opacity: 1; transform: scale(1); } }
@keyframes countUp { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }
@keyframes pulseStep { 0%,100% { box-shadow: 0 0 0 0 rgba(15,118,110,0.4); } 50% { box-shadow: 0 0 0 8px rgba(15,118,110,0); } }
@keyframes barGrow { from { width: 0; } }
@keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
@keyframes drawLine { from { stroke-dashoffset: 1000; } to { stroke-dashoffset: 0; } }
```

## UX Principles
1. **Deadline-driven**: Urgency colors permeate every view — green (>30d), amber (<30d), red (<7d)
2. **Financial first**: Every entity shows its funding context — amounts, burn rates, remaining budget
3. **Phase awareness**: Grant lifecycle is always visible, current phase always highlighted
4. **Progressive disclosure**: Summary cards at top, detailed breakdowns below
5. **Cross-linking**: Every person links to their grants, every grant links to its team and institution

---

## Page Wireframes

### 1. dashboard.html — Financial Overview
```
+--sidebar--+-------------------------------------------+
|  Logo      |  [Total Funding €4.2M] [Active Grants 6] |
|  Overview* |  [Burn Rate 52%]       [Overdue Reports 2]|
|  People    |-------------------------------------------|
|  Research  |  [Donut: By Funder]  [Monthly Spend Line] |
|  Events    |-------------------------------------------|
|  Partners  |  [Upcoming Deadlines - urgency colored]   |
|            |  [Grant Phase Distribution - horiz bar]   |
+------------+-------------------------------------------+
```
- **Top row**: 4 summary cards with animated counters + trend arrows
- **Middle row**: SVG donut chart (DFG/ERC/BMBF/DAAD/EU segments) + sparkline area chart
- **Bottom row**: Deadline list with countdown badges + stacked horizontal bar for phase distribution

### 2. listing.html — Persons Table
```
+--sidebar--+-------------------------------------------+
|            |  Persons (18)          [Search] [Sort by] |
|            |-------------------------------------------|
|            |  Name | Institution | Grants | Funding |  |
|            |  -----------------------------------------|
|            |  Dr. Amina Osei | UBT | 3 | €560K | ... |
|            |  Prof. Kwame... | Legon | 2 | €380K |    |
|            |  ... animated rows sliding up ...         |
+------------+-------------------------------------------+
```
- Table with sortable columns (default: sort by total funding desc)
- Each row shows: avatar initials, name (link to detail), institution, active grants count, total funding, publications count, primary role
- Animated row entrance with staggered delays

### 3. detail.html — Dr. Amina Osei Profile
```
+--sidebar--+-------------------------------------------+
|            |  < Back to Persons                        |
|            |  [Avatar] Dr. Amina Osei                  |
|            |  Univ. of Bayreuth | PI | €560K total     |
|            |-------------------------------------------|
|            |  [Grant Timeline - horizontal bars]       |
|            |  [Publications by Year - bar chart]       |
|            |  [Project Roles + Budget Responsibility]  |
|            |  [Upcoming Deadlines]                     |
+------------+-------------------------------------------+
```
- Hero section with name, institution, role, animated funding counter
- Grant participation timeline (horizontal Gantt-like bars per project)
- Publication output animated bar chart (by year)
- Project cards with lifecycle stepper + budget responsibility percentage
- Personal deadline list with urgency coding

### 4. projects.html — Grant Portfolio
```
+--sidebar--+-------------------------------------------+
|            |  Grant Portfolio (6)                      |
|            |  [Filter: Phase] [Filter: Funder]         |
|            |-------------------------------------------|
|            |  +--card--+ +--card--+ +--card--+         |
|            |  |Stepper | |Stepper | |Stepper |         |
|            |  |Donut   | |Donut   | |Donut   |         |
|            |  |Team    | |Team    | |Team    |         |
|            |  +--------+ +--------+ +--------+         |
+------------+-------------------------------------------+
```
- Filter bar: phase dropdown, funder dropdown, section dropdown
- 2-column or 3-column card grid
- Each card: project name, funder badge, lifecycle stepper (animated), mini donut chart (spent vs remaining), team member avatars, next milestone date, budget amount

### 5. events.html — Academic Calendar
```
+--sidebar--+-------------------------------------------+
|            |  Academic Calendar                        |
|            |  [Countdown Cards - next 3 events]       |
|            |-------------------------------------------|
|            |  [Timeline with animated nodes]           |
|            |  [Upcoming Deadlines sidebar]             |
|            |  [Event Type Distribution - mini bars]    |
+------------+-------------------------------------------+
```
- Top: 3 countdown cards for nearest events (animated number display, urgency colored)
- Main: Vertical timeline with animated dot nodes, event cards alternating left/right
- Sidebar panel: upcoming submission deadlines
- Mini horizontal bar chart: events by type (conference, workshop, symposium, etc.)

### 6. institutions.html — Partner Financial Overview
```
+--sidebar--+-------------------------------------------+
|            |  Partner Network (8)                      |
|            |  [Total Funding Received] [Active Grants] |
|            |-------------------------------------------|
|            |  +--card--+ +--card--+                    |
|            |  |Inst    | |Inst    |  [Collab Strength] |
|            |  |Funding | |Funding |  [animated bars]   |
|            |  |Grants  | |Grants  |                    |
|            |  +--------+ +--------+                    |
+------------+-------------------------------------------+
```
- Summary cards: total partner funding, active partnerships, average grant size
- Institution cards sorted by funding volume: name, country, total funding (animated counter), active grants count, collaboration strength bar
- Geographic badge (Africa/Europe/Americas)
- Animated collaboration strength horizontal bars

## Unique Features
1. **Grant Lifecycle Stepper**: Horizontal 6-step stepper (Application > Review > Funded > Active > Reporting > Closed) with pulse animation on current phase
2. **Animated Financial Counters**: All monetary values count up from 0 using Alpine.js x-init
3. **SVG Donut Charts**: Pure CSS/SVG animated donuts showing budget allocation by funder and spent vs remaining
4. **Urgency Color System**: Deadline proximity automatically determines badge color (green/amber/rose)
5. **Sparkline Charts**: Inline SVG sparklines for monthly expenditure trends
6. **Funder Badges**: Color-coded badges for DFG (teal), ERC (sky), BMBF (amber), DAAD (violet), EU Horizon (indigo)

## Data Reference

### Projects with Funding
| Project | Funder | Budget | Spent % | Phase |
|---------|--------|--------|---------|-------|
| Transnational Migration | DFG | €380K | 75% | Active |
| Decolonizing Knowledge | ERC | €1.2M | 25% | Active |
| Climate Adaptation | BMBF | €450K | 85% | Reporting |
| Visual Cultures | DFG | €290K | 50% | Active |
| Language & Power | DAAD | €180K | 15% | Funded |
| Digital Heritage | EU Horizon | €890K | 5% | Application |

### Key People (with grant involvement)
| Name | Institution | Grants | Total Funding | Publications | Role |
|------|-------------|--------|---------------|-------------|------|
| Dr. Amina Osei | Univ. of Bayreuth | 3 | €560K | 24 | PI |
| Prof. Kwame Asante | Univ. of Ghana, Legon | 2 | €380K | 31 | Co-PI |
| Dr. Fatou Diallo | Cheikh Anta Diop Univ. | 2 | €320K | 18 | PI |
| Prof. Elena Rossi | Sapienza Univ. Rome | 1 | €290K | 22 | PI |
| Dr. Yusuf Ibrahim | Univ. of Cape Town | 2 | €450K | 15 | Co-PI |
| Prof. Aisha Mwangi | Univ. of Nairobi | 1 | €180K | 27 | PI |
| Dr. Jean-Pierre Kouadio | Univ. Felix Houphouet-Boigny | 1 | €120K | 12 | PostDoc |
| Prof. Hans Mueller | Univ. of Bayreuth | 2 | €890K | 35 | PI |

### Institutions
| Institution | Country | Funding | Grants |
|-------------|---------|---------|--------|
| Univ. of Bayreuth | Germany | €1.82M | 5 |
| Univ. of Ghana, Legon | Ghana | €580K | 3 |
| Cheikh Anta Diop Univ. | Senegal | €520K | 2 |
| Univ. of Cape Town | South Africa | €450K | 2 |
| Sapienza Univ. Rome | Italy | €290K | 1 |
| Univ. of Nairobi | Kenya | €280K | 2 |
| Univ. Felix Houphouet-Boigny | Cote d'Ivoire | €180K | 1 |
| Moi University | Kenya | €120K | 1 |

### Events (with deadlines)
| Event | Date | Type | Deadline |
|-------|------|------|----------|
| DFG Annual Report | Mar 15, 2026 | Report | 25 days |
| BMBF Mid-term Review | Apr 3, 2026 | Review | 44 days |
| African Studies Conference | May 22, 2026 | Conference | 93 days |
| ERC Progress Report | Jun 10, 2026 | Report | 112 days |
| Workshop: Digital Methods | Jul 20, 2026 | Workshop | 152 days |
| Cluster Retreat | Sep 18, 2026 | Retreat | 212 days |
| EU Horizon Proposal Deadline | Feb 28, 2026 | Deadline | 10 days |
| DAAD Fellowship Submission | Nov 25, 2026 | Deadline | 280 days |
