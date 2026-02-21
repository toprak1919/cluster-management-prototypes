# Style N: Research Showcase Platform — Design Plan

## Design Philosophy
A bold, outward-facing academic showcase inspired by TED.com, Behance, and premium conference websites. The design prioritizes visual impact through alternating dark/light sections, large typography, and scroll-triggered animations. Every section is a "stage" that reveals itself as the user scrolls, creating a cinematic presentation of research excellence.

## Color System
| Role | Color | Hex | Usage |
|------|-------|-----|-------|
| Primary Dark | Deep Charcoal | `#1a1a2e` | Hero sections, dark backgrounds, nav solid state |
| Primary Light | Crisp White | `#ffffff` | Content sections, cards, text on dark |
| Accent | Coral Red | `#e94560` | CTAs, highlights, active states, badges |
| Secondary Text | Cool Gray | `#94a3b8` | Captions, metadata, secondary info |
| Section Colors | UBT Green | `#0d9462` | Knowledge section tags |
| Section Colors | Azure | `#008f9c` | Methodology section tags |
| Section Colors | Raspberry | `#bd62a0` | Society section tags |
| Section Colors | Purple | `#787acd` | Culture section tags |
| Surface | Slate 50 | `#f8fafc` | Alternate light backgrounds |

## Typography
- **Font**: Inter (Google Fonts) — weights 300, 400, 500, 600, 700
- **Display Headlines**: `text-5xl font-light tracking-tight` (hero titles)
- **Section Headers**: `text-3xl font-semibold` on white, `text-3xl font-light` on dark
- **Card Titles**: `text-xl font-semibold`
- **Body**: `text-base font-normal leading-relaxed`
- **Captions/Meta**: `text-sm text-gray-400`
- **Line Heights**: Generous (leading-relaxed, leading-loose for body text)

## Navigation
- **Type**: Sticky top nav bar, full-width
- **Initial State**: Transparent background over charcoal hero
- **Scrolled State**: Solid white with subtle shadow (CSS transition via Alpine scroll watcher)
- **Elements**: Wordmark "AFRICA MULTIPLE" (left) + nav links (center) + search icon + "All Prototypes" link (right)
- **Mobile**: Hamburger collapse with slide-down menu
- **Active Page**: Coral-red underline or text color

## Animation Strategy
All animations use CSS transitions + Alpine.js `x-intersect` for scroll triggering:

1. **Hero Fade-In**: Page-load animation, content fades up from 30px below (0.8s ease-out)
2. **Section Reveal**: Each full-width section fades/slides up when entering viewport (0.8s ease-out, staggered children at 0.1s intervals)
3. **Counter Animation**: Numbers count from 0 to target when visible (Alpine x-intersect + setInterval)
4. **Bar Expand**: Progress/metric bars scale from 0 to target width (CSS transform scaleX, 1.2s ease-out)
5. **Node Reveal**: Timeline nodes scale from 0 to 1 when scrolled to (0.5s each, staggered)
6. **Card Stagger**: Grid cards animate in with 0.1s delay between each
7. **Hover Effects**: Cards lift with shadow on hover (transform translateY -4px + shadow-xl)

## UX Principles
- **Rhythm**: Alternating charcoal/white sections create visual rhythm and prevent monotony
- **Progressive Disclosure**: Content reveals as user scrolls, rewarding exploration
- **Typography-First**: Large display type creates hierarchy without relying on images
- **High Contrast**: White-on-charcoal and charcoal-on-white ensure readability
- **Conference Feel**: Speaker cards, event countdowns, and showcase layouts evoke premium academic events

## Unique Features
- Animated stat counters (count-up effect on scroll)
- Alternating dark/light full-bleed sections
- Conference-speaker-card format for researchers
- Horizontal scroll showcase for events
- Portfolio-style project case studies
- Animated progress/metric bars
- Timeline with node reveals for events
- Keyword cloud with animated reveal

---

## Page Wireframes

### 1. dashboard.html — Showcase Home
```
[STICKY NAV - transparent over hero]
[=== HERO (charcoal bg, full-width) ===]
  "Africa Multiple"  (text-6xl font-light white)
  "Cluster of Excellence"  (text-2xl font-light gray-400)
  [3 animated counters: 847 Researchers | 23 Projects | 38 Countries]
  [CTA: "Explore Research" coral button]

[=== FEATURED PROJECTS (white bg) ===]
  "Featured Research" section header
  [3 project cards in grid - title, section tag, description, metrics]

[=== RESEARCH HIGHLIGHTS (charcoal bg) ===]
  "Research Impact" header (white)
  [Publication metrics with animated horizontal bars]
  [Stats: Total Publications, Avg Citations, H-Index]

[=== UPCOMING EVENTS (white bg) ===]
  "Upcoming Events" header
  [Horizontal scroll row of event cards with date, title, type]

[=== PARTNERS (slate bg) ===]
  Partner institution logos/names strip

[FOOTER]
```

### 2. listing.html — Researcher Directory
```
[STICKY NAV]
[=== HERO (charcoal bg, shorter) ===]
  "Our Researchers" (text-5xl font-light)
  "847 researchers across 38 countries"
  [Search bar]

[=== FILTERS (white bg, sticky below nav) ===]
  Section filter tabs: All | Knowledge | Society | Culture | Methodology

[=== RESEARCHER GRID (white bg) ===]
  [Cards in 3-col grid, staggered animation]
  Each card:
    - Large initials circle (section-colored border)
    - Name (text-xl font-semibold)
    - Title + Institution
    - Research keyword tags
    - Publication count badge
    - Hover: lift + shadow

[FOOTER]
```

### 3. detail.html — Researcher Spotlight (Dr. Amina Osei)
```
[STICKY NAV]
[=== HERO (charcoal bg, tall) ===]
  Breadcrumb: Researchers > Dr. Amina Osei
  "Dr. Amina Osei" (text-5xl font-light white)
  "Associate Professor of Cultural Anthropology"
  University of Ghana | Section: Culture
  [Contact/Profile links]

[=== RESEARCH FOCUS (white bg) ===]
  "Research Focus" header
  Keyword cloud (animated reveal, varying sizes)
  Research statement paragraph

[=== PROJECTS (slate bg) ===]
  "Projects" header
  Portfolio-style case study cards (image placeholder + title + desc + metrics)

[=== PUBLICATIONS (white bg) ===]
  "Publications" header
  Citation-style list with impact factor indicators (animated bars)

[=== EVENTS (charcoal bg) ===]
  "Event Timeline" header (white)
  Animated vertical timeline with node reveals

[=== COLLABORATIONS (white bg) ===]
  "Collaborations" header
  Partner institution cards

[FOOTER]
```

### 4. projects.html — Research Portfolio
```
[STICKY NAV]
[=== HERO (charcoal bg) ===]
  "Research Portfolio" (text-5xl font-light)
  "23 interdisciplinary projects"
  [Status filter pills: All | Active | Completed | Planning]

[=== PROJECT SHOWCASE (alternating bg) ===]
  Each project as full-width section, alternating layout:
  - Odd: Content left, visual right
  - Even: Visual left, content right
  Each includes:
    - Project title (text-3xl)
    - Section tag badge
    - Description paragraph
    - Progress bar (animated)
    - Team member avatars
    - Funding badge
    - Duration/status

[FOOTER]
```

### 5. events.html — Event Showcase
```
[STICKY NAV]
[=== HERO — NEXT EVENT (charcoal bg, tall) ===]
  "Next Event" label
  Event title (text-5xl font-light)
  Countdown timer (days : hours : minutes : seconds)
  Date, location, type
  [CTA: "Register Now" coral button]

[=== UPCOMING EVENTS (white bg) ===]
  "Upcoming Events" header
  [Cards grid with date overlay, title, type badge, location]

[=== PAST EVENTS (slate bg) ===]
  "Event Archive" header
  Monthly horizontal timeline
  Visual archive grid with cards

[FOOTER]
```

### 6. institutions.html — Partner Showcase
```
[STICKY NAV]
[=== HERO (charcoal bg) ===]
  "Global Research Network" (text-5xl font-light)
  [3 animated counters: 156 Institutions | 38 Countries | 5 Continents]

[=== INSTITUTION GRID (white bg, by continent) ===]
  Continent section dividers with animated reveals
  "Africa" header with count
  [Institution cards: name, country, member count, project count, "Since" badge]

  "Europe" header with count
  [Institution cards...]

  (repeat for each continent)

[FOOTER]
```

## Technical Stack
- **Tailwind CSS**: CDN (`https://cdn.tailwindcss.com`)
- **Alpine.js**: CDN (`https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js`)
- **Font**: Inter via Google Fonts
- **No images**: All visuals via CSS/SVG/initials
- **Responsive**: Mobile-first, 3-col -> 2-col -> 1-col grids
- **Cross-linked**: All 6 pages linked via nav, plus back-to-prototypes link
