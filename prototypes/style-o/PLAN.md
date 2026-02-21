# Style O: Academic Operations Center — Design Plan

## Design Philosophy

Mission control meets modern ops dashboard. Inspired by tools like Datadog, Grafana, and PagerDuty — but tailored for academic research cluster management. Every pixel communicates system health, data freshness, and operational status. The interface feels "alive" with pulsing indicators, streaming feeds, and auto-updating timestamps. Information density is high but never overwhelming — the dark theme reduces visual noise while bright data colors draw attention to what matters.

## Color System

| Token | Hex | Usage |
|-------|-----|-------|
| Background | `#0f172a` (slate-900) | Main page background |
| Surface | `#1e293b` (slate-800) | Cards, panels, widgets |
| Surface elevated | `#334155` (slate-700) | Hover states, secondary surfaces |
| Border | `#475569` (slate-600) | Subtle borders between elements |
| Text primary | `#f1f5f9` (slate-100) | Headings, metric values |
| Text secondary | `#94a3b8` (slate-400) | Labels, descriptions |
| Text muted | `#64748b` (slate-500) | Timestamps, tertiary info |
| Cyan (Primary) | `#06b6d4` | Primary metrics, active nav, links |
| Emerald (Healthy) | `#10b981` | Healthy status, uptime, success |
| Amber (Warning) | `#f59e0b` | Warnings, deadlines approaching |
| Rose (Critical) | `#f43f5e` | Critical alerts, overdue, errors |
| Violet (Info) | `#8b5cf6` | Secondary accent, charts, badges |

## Typography

- **Font**: Inter (Google Fonts), system-ui fallback
- **Metric values**: text-3xl/4xl font-bold, bright color (cyan/emerald/amber)
- **Section headers**: text-sm font-semibold uppercase tracking-wider, slate-400
- **Body text**: text-sm, slate-300
- **Monospace data**: font-mono for timestamps, IDs, counts
- **Navigation labels**: text-xs font-medium

## Navigation

### Top Bar (h-12, bg-slate-900, border-b border-slate-700)
- Left: Logo icon + "Africa Multiple" text + breadcrumb trail (slate-400 > slate-200)
- Center: Omni-search bar (slate-800 bg, rounded-lg, w-96)
- Right: Live indicator (pulsing green dot + "Live"), notification bell with count badge, user avatar

### Left Icon Rail (w-14, bg-slate-900, border-r border-slate-800)
- Vertical icon strip with tooltip labels on hover
- Icons: Dashboard (grid), Persons (users), Projects (folder), Events (calendar), Institutions (building)
- Active state: cyan background pill behind icon
- Bottom: Settings gear + "All Prototypes" link

## Animation Strategy

### Core Animations
1. **pulseAlive**: Pulsing dots for live status indicators (2s ease-in-out infinite)
2. **slideInMetric**: Metric cards slide up and fade in on load (0.4s ease-out, staggered delays)
3. **sparklineDraw**: SVG sparklines draw themselves via stroke-dashoffset
4. **gaugeRotate**: Progress rings animate from 0 to target angle
5. **streamIn**: Activity feed items stream in from left with expanding height
6. **countUp**: Numeric values count up from 0 to target (Alpine.js x-init with setInterval)
7. **barGrow**: CSS bar chart bars grow from 0 height/width to target

### Timing Strategy
- Cards load with 0.1s stagger (card-1: 0s, card-2: 0.1s, card-3: 0.2s...)
- Metrics count up over 1.5s after card appears
- Sparklines draw over 1s
- Activity feed adds new items every 5-8s (simulated)

## Per-Page Wireframes

### 1. dashboard.html — Operations Overview

```
[Top Bar: Logo | Breadcrumb: Dashboard | Search | Live ● | Bell(3) | Avatar]
[Rail] [=== Status Banner: "All Systems Operational" ● 99.8% uptime === ]
[Rail] [ Metric: Active    ][ Metric: Projects ][ Metric: Events  ][ Metric: Data     ]
[Rail] [ Researchers  847  ][ Health    23 act  ][ Upcoming  5     ][ Quality  92%      ]
[Rail] [ ▲ +12 this mo     ][ ●● 2 warnings    ][ Next: 3 days    ][ gauge animation   ]
[Rail] [                   ]                     [                  ][                   ]
[Rail] [ Budget Status     ][ Recent Activity (streaming feed)     ][ Deadline Alerts   ]
[Rail] [ Donut: 68% spent  ][ ● Dr. Osei updated profile  2s ago  ][ ⚠ Report due 3d   ]
[Rail] [                   ][ ● New project created       15s ago  ][ ⚠ Approval needed ]
[Rail] [                   ][ ● Event registration opened  1m ago  ][ ● Review due 7d   ]
[Rail] [                   ][                                      ][                   ]
[Rail] [ System Stats      ][ Sync: 2m ago | Records: 847 | DB: 12ms | Cache: 98.2%    ]
```

Widgets: 8 total in a 12-col grid. Top row: 4x 3-col metric cards. Middle: 3-col budget donut + 6-col activity feed + 3-col deadline alerts. Bottom: full-width system stats bar.

### 2. listing.html — Persons Operations Table

```
[Top Bar: Logo | Breadcrumb: Dashboard > Persons | Search | Live ● | Bell | Avatar]
[Rail] [ Quick Stats: 847 Total | 612 Active | 23 New this month | 92% Profiles Complete ]
[Rail] [ Search _________ | Filter: Section ▼ | Institution ▼ | Status ▼ | + Add Person ]
[Rail] [━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━]
[Rail] [ ● Dr. Amina Osei    | a.osei@ug..  | U of Ghana  | Mobilities | Active ● | ▃▅▇ ]
[Rail] [ ● Prof. K. Asante   | k.asante@..  | U Cape Town | Knowledges | Active ● | ▂▄▆ ]
[Rail] [ ● Dr. F. Diallo     | f.diallo@..  | U Dakar     | Moralities | Active ● | ▁▃▅ ]
[Rail] [ ... more rows with inline sparklines, status dots, last-seen timestamps ...     ]
```

Dark table with bright text. Each row has: status dot (green/amber/red), name, email, institution, research section, membership status, activity sparkline (last 30 days), "last seen" timestamp. Sortable columns. Animated row loading (stagger from top).

### 3. detail.html — Dr. Amina Osei Profile Dashboard

```
[Top Bar: Logo | Breadcrumb: Dashboard > Persons > Dr. Amina Osei | ... ]
[Rail] [ Profile Card: Avatar AO | Dr. Amina Osei | U of Ghana | Status badges      ]
[Rail] [                          | Senior Researcher | Mobilities | Active since 2020 ]
[Rail] [━━━━━ Personal KPIs ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━]
[Rail] [ Pubs This Year ][ Active Projects ][ h-index ][ Events Attended ][ Collab.   ]
[Rail] [      12 ▲       ][       4         ][   18    ][       8         ][ 15 people ]
[Rail] [                                                                              ]
[Rail] [ Activity Heatmap (GitHub-style contribution grid — 52 weeks)                 ]
[Rail] [ ░░▓▓░░▓░░░▓▓▓░░░▓░▓▓░░░▓░░░▓▓░░▓▓░░░▓░▓▓▓░░░▓░▓░░▓▓░       ]
[Rail] [                                                                              ]
[Rail] [ Project Timeline (horiz bars)  ][ Contact Info      ][ Publication Chart     ]
[Rail] [ ━━━━ Project A ━━━━━           ][ Email, Phone...   ][ Bar chart by year     ]
[Rail] [ ━━━━━━ Project B ━━━━━━━━      ][ ORCID, Web        ][ 2022: ██████  8      ]
[Rail] [   ━━━ Project C ━━━            ][                    ][ 2023: ████████ 10    ]
[Rail] [                                ][ Event Attendance   ][ 2024: ██████████ 12  ]
```

### 4. projects.html — Project Status Board

```
[Top Bar: Logo | Breadcrumb: Dashboard > Projects | ... ]
[Rail] [ Health Overview: 23 Total | 15 On Track ● | 5 Delayed ⚠ | 3 At Risk ● ]
[Rail] [                                                                         ]
[Rail] [ Planned (3)     ][ Active (12)      ][ Reporting (5)   ][ Completed (3) ]
[Rail] [ ┌─────────────┐ ][ ┌──────────────┐ ][ ┌─────────────┐][ ┌────────────┐]
[Rail] [ │ Project Alpha│ ][ │ Project Beta │ ][ │ Project Eta │][ │ Project Mu │]
[Rail] [ │ ● Planned    │ ][ │ ● On Track   │ ][ │ ⚠ Delayed   │][ │ ✓ Complete │]
[Rail] [ │ ████░░ 60%   │ ][ │ ████████ 82% │ ][ │ ██████░ 70% │][ │ ██████████ │]
[Rail] [ │ Budget: 45%  │ ][ │ Budget: 68%  │ ][ │ Budget: 89% │][ │ Budget: 95%│]
[Rail] [ │ Team: 5      │ ][ │ Team: 8      │ ][ │ Team: 4     │][ │ Team: 6    │]
[Rail] [ │ Due: Mar 2026│ ][ │ Due: Jun 2026│ ][ │ Due: Overdue│][ │ Completed  │]
[Rail] [ └─────────────┘ ][ └──────────────┘ ][ └─────────────┘][ └────────────┘]
```

Kanban columns. Cards have: health dot, project name, progress bar (animated), burn rate, team count, next deadline. Sidebar with animated gauge charts for on-track/delayed/at-risk counts.

### 5. events.html — Event Operations

```
[Top Bar: Logo | Breadcrumb: Dashboard > Events | ... ]
[Rail] [ Quick Stats: 5 Upcoming | 12 This Year | 847 Total Attendees | 3 Types ]
[Rail] [                                                                         ]
[Rail] [ Countdown Cards (next 3 events)                                         ]
[Rail] [ ┌──────────────────┐┌──────────────────┐┌──────────────────┐            ]
[Rail] [ │ Workshop: Digital │ │ Conference: Ann. │ │ Seminar: Methods │           ]
[Rail] [ │  03d 14h 22m 08s │ │  12d 06h 45m 31s │ │  28d 19h 03m 52s│           ]
[Rail] [ │ Capacity: ██████░ │ │ Capacity: ████░░ │ │ Capacity: ██░░░░│           ]
[Rail] [ │ 45/60 registered │ │ 120/200 reg.     │ │ 15/40 reg.      │           ]
[Rail] [ └──────────────────┘└──────────────────┘└──────────────────┘            ]
[Rail] [                                                                         ]
[Rail] [ Past Events Table          ][ Monthly Heatmap Calendar ][ Type Distrib. ]
[Rail] [ Name | Date | Attendance   ][ Jan ░░▓░░░░ Feb ░▓▓░░   ][ Workshop  40% ]
[Rail] [ Workshop AI | 2025-11 | 58 ][ Mar ░░░░░░░ Apr ▓░░▓░   ][ Conf.     35% ]
[Rail] [ Conference  | 2025-09 |180 ][ May ░▓░░░░░ Jun ░░▓░░   ][ Seminar   25% ]
```

### 6. institutions.html — Partner Operations

```
[Top Bar: Logo | Breadcrumb: Dashboard > Institutions | ... ]
[Rail] [ Quick Stats: 24 Partners | 8 Countries | 3 Continents | 156 Active Collabs ]
[Rail] [                                                                              ]
[Rail] [ Collaboration Heatmap Matrix (institutions x research sections)              ]
[Rail] [              Moralities | Mobilities | Knowledges | Aesthetics | Learning     ]
[Rail] [ U of Ghana        ██       ████          ██           ░░         ░░           ]
[Rail] [ U Cape Town        ░░       ██           ████          ██         ██          ]
[Rail] [ KNUST              ██       ░░            ██          ████        ██          ]
[Rail] [ U Nairobi          ░░       ██            ██           ██        ████         ]
[Rail] [                                                                              ]
[Rail] [ Institution Table (sortable)       ][ Geographic Distribution ][ Health     ]
[Rail] [ Name | Country | Researchers | ▃▅▇ ][ Africa ████████ 65%     ][ Active: 20 ]
[Rail] [ U Ghana | Ghana | 45 | sparkline   ][ Europe █████ 25%        ][ Review: 3  ]
[Rail] [ UCT | S.Africa | 38 | sparkline    ][ Americas ██ 10%         ][ Inactive: 1]
```

## UX Principles

1. **Glanceability**: Key health metrics visible within first second of page load
2. **Progressive disclosure**: Summary first, drill down for detail
3. **Temporal awareness**: Every data point communicates freshness ("2s ago", "Updated just now")
4. **Status-first**: Every entity has a visible health status (green/amber/red dot)
5. **Scannable density**: High information density but with clear visual hierarchy through color and size
6. **Motion with purpose**: Animations indicate live data, not decoration

## Unique Features

1. **Live status banner**: Top-of-page operational status with uptime percentage
2. **Streaming activity feed**: Auto-scrolling feed with new items appearing with animation
3. **Animated counters**: Metric values count up from 0 on page load
4. **GitHub-style contribution heatmap**: Activity visualization on person detail
5. **Kanban project board**: Drag-feel column layout for project status
6. **Countdown timers**: Ticking real-time countdown for upcoming events
7. **Collaboration intensity heatmap**: Matrix showing partner/section relationships
8. **Sparkline inline charts**: Tiny SVG line charts embedded in table rows
9. **Progress rings**: Animated circular gauges for completion metrics
10. **System stats bar**: Always-visible bottom bar with sync time, record counts, latency

## Technical Stack

- Tailwind CSS via CDN (dark theme utilities)
- Alpine.js for interactivity (counters, filters, toggles, timers)
- Pure CSS animations (keyframes for pulse, slide, draw)
- Inline SVG for sparklines, gauges, heatmaps
- No external images — initials-based avatars, SVG icons
- Responsive: icon rail collapses on mobile, grid adapts to columns
- All pages cross-linked with consistent navigation
