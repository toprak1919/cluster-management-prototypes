# Style M: Academic Collaboration Hub — Design Plan

## Design Philosophy
A team-focused research management tool inspired by Slack, ResearchGate, and Figma's collaborative feel. The design centers on **who is working on what** — showing real-time presence, activity feeds, and collaboration networks. Every element communicates connection and teamwork.

## Color System
| Token | Value | Usage |
|-------|-------|-------|
| Primary (violet-700) | `#6d28d9` | Interactive elements, active states, primary actions |
| Primary light (violet-50) | `#f5f3ff` | Subtle highlights, hover states |
| Primary medium (violet-100) | `#ede9fe` | Selected sidebar items, badges |
| Background | `#f8fafc` (slate-50) | Page background |
| Surface | `#ffffff` | Cards, panels |
| Active/Online | `#10b981` (emerald-500) | Online indicators, success states |
| Pending/Warning | `#f59e0b` (amber-500) | Pending states, deadlines |
| Text primary | `#0f172a` (slate-900) | Headings |
| Text secondary | `#64748b` (slate-500) | Body text |
| Text muted | `#94a3b8` (slate-400) | Timestamps, metadata |
| Border | `#e2e8f0` (slate-200) | Card borders, dividers |

## Typography
- **Font**: Inter (Google Fonts) — clean, modern, collaborative feel
- **Headings**: font-semibold/bold, slate-900
- **Body**: font-normal, slate-600
- **Metadata/timestamps**: text-xs, slate-400
- **Activity text**: text-sm with bold actor names

## Navigation — Left Sidebar (w-56)
Fixed left sidebar designed like a team workspace:
1. **Workspace switcher** at top — "Africa Multiple Cluster" with dropdown icon
2. **Main sections** with icons + count badges:
   - Home (dashboard)
   - People (42)
   - Projects (23)
   - Events (18)
   - Partners (15)
3. **User avatar + status** at bottom — name, role, online dot
4. Active page highlighted with violet-100 bg + violet-700 text
5. Sidebar collapses to icons on mobile (responsive)

## Animation Strategy
All animations are subtle, purposeful, and enhance the collaborative feel:

### Core Animations
```css
@keyframes slideUp { from { opacity: 0; translateY(15px) } to { opacity: 1; translateY(0) } }
@keyframes popIn { from { opacity: 0; scale(0.8) } to { opacity: 1; scale(1) } }
@keyframes pulseOnline { 0%,100% { opacity: 1 } 50% { opacity: 0.5 } }
@keyframes progressRing { from { stroke-dashoffset: 283 } }
@keyframes feedItem { from { opacity: 0; translateX(-10px) } to { opacity: 1; translateX(0) } }
@keyframes countUp { from { opacity: 0; translateY(12px) } to { opacity: 1; translateY(0) } }
```

### Usage
- **Card entrance**: slideUp with staggered delays (0.05s increments)
- **Activity feed items**: feedItem with staggered delays
- **Online indicators**: pulseOnline continuous
- **Progress rings**: progressRing on load (SVG)
- **Stat counters**: countUp with Alpine.js x-intersect
- **Hover**: scale(1.02) + shadow increase on cards

## Per-Page Wireframes

### 1. dashboard.html — Collaboration Home
```
┌─────────┬───────────────────────────────────────────┐
│ SIDEBAR │  Activity Feed         │  Your Team (6)   │
│         │  ┌─────────────────┐  │  ┌──┐┌──┐┌──┐    │
│ Home*   │  │ AO updated...   │  │  │AO││KA││FD│    │
│ People  │  │ KA added pub... │  │  └──┘└──┘└──┘    │
│ Projects│  │ SM joined...    │  │  ┌──┐┌──┐┌──┐    │
│ Events  │  │ ... (10 items)  │  │  │SM││JH││CB│    │
│ Partners│  └─────────────────┘  │  └──┘└──┘└──┘    │
│         │───────────────────────┤───────────────────│
│         │  Active Projects (3)  │  Upcoming Events  │
│         │  ┌─────────────────┐  │  ┌─────────────┐  │
│  User   │  │ Ring  Title     │  │  │ Conference   │  │
│  avatar │  │ Team  Activity  │  │  │ Workshop     │  │
│  status │  └─────────────────┘  │  └─────────────┘  │
│         │  Quick Stats (animated counters)           │
└─────────┴───────────────────────────────────────────┘
```

### 2. listing.html — People Directory
```
┌─────────┬──────────────────────────────────────────┐
│ SIDEBAR │  People Directory              42 online │
│         │  [All] [Fellows] [Researchers] [PhD]     │
│         │  ┌──────┐ ┌──────┐ ┌──────┐             │
│         │  │ ● AO │ │ ○ KA │ │ ● FD │             │
│         │  │ UGhana│ │ ULegon│ │ UCAD │             │
│         │  │Working│ │Working│ │Working│             │
│         │  │on:Proj│ │on:Proj│ │on:Proj│             │
│         │  │ 12pub │ │ 8pub  │ │ 15pub │             │
│         │  └──────┘ └──────┘ └──────┘             │
│         │  (4 cols grid, staggered animation)      │
└─────────┴──────────────────────────────────────────┘
```

### 3. detail.html — Dr. Amina Osei Profile
```
┌─────────┬──────────────────────────────────────────┐
│ SIDEBAR │  ┌─ Profile Hero ─────────────────────┐  │
│         │  │ [Avatar]  Dr. Amina Osei           │  │
│         │  │ Collab stats: 8 co-authors, 3 proj │  │
│         │  └────────────────────────────────────┘  │
│         │  [Activity] [Research] [Network] [Events]│
│         │  ┌─ Activity Tab ─────────────────────┐  │
│         │  │ Personal activity feed timeline     │  │
│         │  └────────────────────────────────────┘  │
│         │  ┌─ Network Tab ──────────────────────┐  │
│         │  │ SVG node graph: connections to      │  │
│         │  │ co-authors, projects, institutions  │  │
│         │  └────────────────────────────────────┘  │
└─────────┴──────────────────────────────────────────┘
```

### 4. projects.html — Project Workspace
```
┌─────────┬──────────────────────────────────────────┐
│ SIDEBAR │  Projects    [Board] [Kanban] toggle     │
│         │  ┌─ Project Card ─────────────────────┐  │
│         │  │ ◎ Progress Ring   Title             │  │
│         │  │ [AO][KA][FD]     Section badge     │  │
│         │  │ Recent: AO updated milestone...    │  │
│         │  │ ●──●──●──○──○  milestones          │  │
│         │  │ Deadline: 45 days                  │  │
│         │  └────────────────────────────────────┘  │
│         │  Kanban: Planned | Active | Complete     │
└─────────┴──────────────────────────────────────────┘
```

### 5. events.html — Event Stream
```
┌─────────┬──────────────────────────────────────────┐
│ SIDEBAR │  Events    [Stream] [Timeline] toggle    │
│         │  Upcoming ─────────────────────────────  │
│         │  ┌─ Event Card ───────────────────────┐  │
│         │  │ [Organizer]  Conference Title       │  │
│         │  │ 12 days countdown (animated)       │  │
│         │  │ [att1][att2][att3]+5  Location     │  │
│         │  │ Conference badge                   │  │
│         │  └────────────────────────────────────┘  │
│         │  Past (faded) ─────────────────────────  │
└─────────┴──────────────────────────────────────────┘
```

### 6. institutions.html — Partner Network
```
┌─────────┬──────────────────────────────────────────┐
│ SIDEBAR │  Partner Network                          │
│         │  Most Active Partnerships (top section)   │
│         │  ┌─ Institution Card ─────────────────┐  │
│         │  │ Univ of Ghana    Since 2019        │  │
│         │  │ [AO][KA][SM]    3 active projects  │  │
│         │  │ ████████░░ collab strength bar      │  │
│         │  └────────────────────────────────────┘  │
└─────────┴──────────────────────────────────────────┘
```

## UX Principles
1. **Collaboration visibility**: Always show WHO is working on WHAT
2. **Presence awareness**: Online/offline indicators everywhere
3. **Activity-first**: Recent actions surface to the top
4. **Progressive disclosure**: Cards expand on interaction
5. **Smooth transitions**: Everything animates in/out gracefully
6. **Consistent patterns**: Avatar + action + object + timestamp

## Unique Features
- Real-time activity feed with avatar + action + object pattern
- Presence indicators (green dots, pulse animation)
- SVG progress rings on project cards
- Simple node-graph network visualization (CSS + SVG)
- Stacked avatar groups showing team composition
- Animated stat counters using Alpine.js x-intersect
- Kanban view toggle for projects
- Deadline countdown timers on events
- Collaboration strength bars on institution cards
