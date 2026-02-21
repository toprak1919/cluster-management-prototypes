# Style K: Institutional Portal Pro — Design Plan

## 1. Design Philosophy

University administration tool that feels trusted, professional, and efficient. Inspired by Harvard's digital portals crossed with Asana's task management clarity. Every element conveys institutional authority while remaining approachable and highly usable. The interface should feel like a well-organized dean's office — everything in its place, nothing superfluous.

## 2. Color System

| Token | Hex | Usage |
|-------|-----|-------|
| Navy Primary | `#1e3a5f` | Headers, nav bar, primary buttons, section backgrounds |
| Navy Dark | `#152c49` | Hover states, active nav items |
| Navy Light | `#2a4d7a` | Secondary elements, borders |
| Gold Accent | `#c5973e` | CTAs, highlights, active states, badge counts, progress indicators |
| Gold Light | `#d4a94f` | Hover on gold elements |
| Gold Pale | `#fdf6e9` | Gold-tinted backgrounds |
| White | `#ffffff` | Card backgrounds, content areas |
| Gray 50 | `#f8f9fb` | Page background |
| Gray 100 | `#eef1f5` | Alternate row, subtle dividers |
| Gray 200 | `#dde2ea` | Borders, dividers |
| Gray 400 | `#8c95a4` | Metadata text, icons |
| Gray 600 | `#4a5568` | Body text |
| Gray 800 | `#1a202c` | Headings |
| Success | `#2d8659` | Active/complete statuses |
| Warning | `#d97706` | Approaching deadlines |
| Danger | `#dc2626` | Overdue, critical alerts |

## 3. Typography

System font stack for performance: `'Inter', system-ui, -apple-system, sans-serif`

| Level | Size | Weight | Color |
|-------|------|--------|-------|
| Page Title | 2rem (32px) | 700 | Gray 800 |
| Section Header | 1.25rem (20px) | 600 | Gray 800 |
| Card Title | 1rem (16px) | 600 | Gray 800 |
| Body | 0.875rem (14px) | 400 | Gray 600 |
| Metadata | 0.75rem (12px) | 400 | Gray 400 |
| Badge | 0.75rem (12px) | 600 | White on color bg |

## 4. Navigation Pattern

**Horizontal top nav** fixed at top, navy background:
- Left: Logo/brand "Cluster Management Portal"
- Center: Main nav items — Dashboard, Persons, Projects, Events, Institutions
- Right: Notification bell (with badge count), user avatar/name, quick-action button

**Mega-menu dropdowns**: Hovering each nav item reveals a dropdown panel:
- Quick stats (count of items)
- 3 recent items as links
- Filter shortcuts (e.g., "Active Projects", "Upcoming Events")
- "View All →" link

**Breadcrumb trail**: Below nav on every page, showing: Home > Section > Current Page

## 5. Animation Strategy

| Animation | Usage | Duration | Easing |
|-----------|-------|----------|--------|
| fadeSlideUp | Page sections on load, staggered | 0.5s | ease-out |
| countUp | Stat numbers on dashboard | 1.5s | ease-out |
| milestoneReveal | Timeline nodes appearing | 0.4s | ease-out |
| progressFill | Funding bars, progress bars | 1s | ease-out |
| bellShake | Notification bell on hover | 0.5s | ease-in-out |
| cardHover | Card lift on hover | 0.2s | ease |
| megaMenuSlide | Dropdown menu appear | 0.2s | ease-out |

Stagger: Each section delayed by 0.1s from previous. Cards within sections delayed by 0.05s.

## 6. Per-Page Wireframes

### Page 1: dashboard.html — Portal Home
```
┌──────────────────────────────────────────────┐
│ [Nav: Logo | Dashboard Persons Projects ... ] │
│ [Breadcrumb: Home > Dashboard]                │
├──────────────────────────────────────────────┤
│ Welcome Banner                                │
│ "Welcome back, Dr. Admin" + date + subtitle   │
├──────────┬──────────┬──────────┬─────────────┤
│ Stat Card│ Stat Card│ Stat Card│ Stat Card    │
│ Persons  │ Projects │ Events   │ Institutions │
│ (navy bg,│ (gold #) │          │              │
│  gold #) │          │          │              │
├──────────┴──────────┴──────────┴─────────────┤
│ [Quarter Timeline — horizontal milestone bar] │
├───────────────────────┬──────────────────────┤
│ Project Status Donut  │ Deadline Alerts       │
│ (CSS donut chart)     │ (list with urgency)   │
├───────────────────────┼──────────────────────┤
│ Recent Activity Feed  │ Quick Stats sidebar   │
└───────────────────────┴──────────────────────┘
│ [Quick Actions Floating Bar]                  │
```

### Page 2: listing.html — Persons Directory
```
┌──────────────────────────────────────────────┐
│ [Nav] [Breadcrumb: Home > Persons]           │
├──────────────────────────────────────────────┤
│ Page Header: "Persons Directory" + count      │
│ Search bar + filter buttons (Role, Inst.)     │
├──────────────────────────────────────────────┤
│ Table Header: Name | Role | Institution |     │
│               Department | Status | Last Act. │
├──────────────────────────────────────────────┤
│ Row 1: [Avatar] Dr. Amina Osei | PI | ...    │
│ Row 2: [Avatar] Prof. Kwame Mensah | ...     │
│ ... 12 rows with animated load                │
├──────────────────────────────────────────────┤
│ Pagination: < 1 2 3 ... >                    │
└──────────────────────────────────────────────┘
```

### Page 3: detail.html — Dr. Amina Osei Profile
```
┌──────────────────────────────────────────────┐
│ [Nav] [Breadcrumb: Home > Persons > Dr. Osei]│
├──────────────────────────────────────────────┤
│ Hero: Initials avatar | Name | Role | Inst.  │
│       Contact info | Status badge             │
├──────────────────────────────────────────────┤
│ Tabs: [Profile] [Research] [Activity] [Net.] │
├──────────────────────┬───────────────────────┤
│ Tab Content Area     │ Sidebar:              │
│ (switches per tab)   │ - Academic Metrics    │
│ Profile: bio, dept   │ - h-index, citations  │
│ Research: pubs list  │ - Publications count  │
│ Activity: timeline   │ - Key dates           │
│ Network: collabs     │                       │
└──────────────────────┴───────────────────────┘
```

### Page 4: projects.html — Project Portfolio
```
┌──────────────────────────────────────────────┐
│ [Nav] [Breadcrumb: Home > Projects]          │
├──────────────────────────────────────────────┤
│ Header: "Project Portfolio" + status filters  │
├──────────────────────────────────────────────┤
│ Grid of Project Cards (3 columns):           │
│ ┌────────────────┐                           │
│ │ Project Title   │                          │
│ │ [Milestone Dots: ●──●──◐──○──○]           │
│ │ Funding Bar: [████████░░] 72%              │
│ │ Team: [AO] [KM] [FA] +2                   │
│ │ Status badge | Duration                    │
│ └────────────────┘                           │
│ ... 12 project cards                         │
└──────────────────────────────────────────────┘
```

### Page 5: events.html — Event Calendar
```
┌──────────────────────────────────────────────┐
│ [Nav] [Breadcrumb: Home > Events]            │
├──────────────────────────────────────────────┤
│ Header + View Toggle: [Calendar] [Timeline]  │
├──────────────────────────────────────────────┤
│ Calendar View: Month grid with event dots    │
│ OR                                           │
│ Timeline View: Vertical timeline with nodes  │
│ ├── ● Feb 15 — Workshop on ...              │
│ ├── ● Mar 01 — Conference ...               │
│ └── ○ Apr 10 — Symposium (upcoming)         │
├──────────────────────────────────────────────┤
│ Event Cards with countdown timers            │
│ Registration status indicators               │
└──────────────────────────────────────────────┘
```

### Page 6: institutions.html — Partner Directory
```
┌──────────────────────────────────────────────┐
│ [Nav] [Breadcrumb: Home > Institutions]      │
├──────────────────────────────────────────────┤
│ Header: "Partner Directory" + continent filter│
├──────────────────────────────────────────────┤
│ Section: Africa                              │
│ ┌─────────────┐ ┌─────────────┐             │
│ │ Inst. Card  │ │ Inst. Card  │             │
│ │ Name        │ │ Name        │             │
│ │ Collab Bar  │ │ Collab Bar  │             │
│ │ Key People  │ │ Key People  │             │
│ │ Since 20XX  │ │ Since 20XX  │             │
│ └─────────────┘ └─────────────┘             │
│ Section: Europe                              │
│ ... grouped cards                            │
└──────────────────────────────────────────────┘
```

## 7. UX Principles — WCAG 2.1 AA Compliance

- **Skip-to-content link**: Hidden link at top, visible on focus, jumps to `#main-content`
- **Focus states**: 3px gold outline on all interactive elements (`outline: 3px solid #c5973e`)
- **Color contrast**: All text meets 4.5:1 minimum ratio; large text 3:1
- **Aria labels**: All icons have `aria-label`, decorative elements have `aria-hidden="true"`
- **Logical tab order**: Follows visual reading order; no tabindex > 0
- **Screen reader**: Live regions for dynamic updates (notifications, counters)
- **Keyboard nav**: All dropdowns, tabs, modals operable via keyboard
- **Reduced motion**: `prefers-reduced-motion` disables all animations

## 8. Unique Features

1. **Mega-menu navigation**: Rich dropdown panels with stats, recent items, and shortcuts
2. **Breadcrumb trail**: Contextual navigation on every page
3. **Notification bell**: Animated bell with badge count and dropdown panel
4. **Quick-action floating bar**: Fixed bottom bar with expandable "Quick Add" for new items
5. **Milestone tracker**: Horizontal connected-dot progress for every project
6. **Funding thermometer**: Animated fill bar showing funding progress
7. **Contextual subtitle**: "You are viewing..." descriptor under breadcrumbs
8. **Animated stat counters**: Numbers count up from 0 on page load
