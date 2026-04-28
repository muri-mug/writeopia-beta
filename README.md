# Handoff: Writeopia Beta — Full App Prototype

## Overview

Writeopia is a productivity SaaS focused on local-model AI for security-sensitive teams (devs, writers, researchers, legal, compliance). All AI inference runs locally via Ollama — no data leaves the machine.

This handoff covers the full app prototype built in this design session:
- **Onboarding flow** (5 steps)
- **Home dashboard** (document grid + sidebar)
- **Document editor** (block editor with AI inline, slash commands, @ mention)
- **Notifications panel** (team activity feed)
- **Settings screen** (Ollama health, model library, profile, workspace, security)

---

## About the Design Files

The files in this bundle are **high-fidelity HTML prototypes** — they show intended look, interactions, and behavior. They are **not production code to ship directly**.

Your task is to **recreate these designs in your target codebase** using its existing framework, component library, and patterns. If no codebase exists yet, React + TypeScript is recommended given the component complexity.

The prototype uses inline React/Babel — treat it as a living spec, not source code.

---

## Fidelity

**High-fidelity.** Pixel-perfect mockups with final colors, typography, spacing, and interactions. Recreate the UI as closely as possible using your codebase's existing libraries and patterns.

---

## Design Tokens

### Colors
```
accent:        #7c3aed   (primary purple)
accentLight:   #9b6dff   (dark mode accent)
accentBg:      #f3f0ff   (purple tint bg)
accentBorder:  #e9d5ff   (purple border)

-- Light mode --
bg:            #faf9fd
surface:       #ffffff
surfaceAlt:    #f5f3fb
border:        #ede9f8
text:          #111827
textMid:       #4b5563
textMuted:     #9ca3af

-- Dark mode --
bg:            #111318
surface:       #1c1e26
surfaceAlt:    #21232e
border:        #2a2d3e
text:          #f1f0f5
textMid:       #a0a3b8
textMuted:     #5c6080

-- Semantic --
success:       #10b981
warning:       #f59e0b
error:         #ef4444
```

### Typography
```
Font: Inter (400, 500, 600, 700, 800)
Fallback: system-ui, sans-serif

Scale:
  xs:   10px / 400
  sm:   11px / 500
  base: 13px / 400–600
  md:   14–15px / 400–600
  lg:   16–18px / 700–800
  xl:   20–28px / 800
  2xl:  32px / 800, letter-spacing: -0.03em
```

### Spacing
```
4px, 6px, 8px, 10px, 12px, 14px, 16px, 20px, 24px, 28px, 32px, 40px, 48px
```

### Border Radius
```
pill:    9999px
button:  9px
card:    14–16px
input:   9px
badge:   20px
icon:    7–8px
avatar:  50%
```

### Shadows
```
card-hover:  0 8px 28px rgba(124,58,237,0.13)
panel:       0 12px 40px rgba(0,0,0,0.15)
modal:       0 20px 60px rgba(0,0,0,0.20)
button:      0 2px 10px rgba(124,58,237,0.30)
sidebar:     2px 0 12px rgba(0,0,0,0.04)
toggle:      0 1px 6px rgba(0,0,0,0.10)
```

---

## Screens

---

### 1. Onboarding Flow

**Purpose:** First-time setup — creates profile, workspace, invites team, connects Ollama.

**Layout:** Full-screen centered card (520px wide), white background with subtle purple radial gradient orbs behind.

**Steps (carousel with progress bar):**

#### Step 1 — Welcome
- Logo: 72px circle with gradient `#7c3aed → #a855f7`, letter "W" at 28px/800
- Title: "Welcome to **Writeopia**" — 32px/800, accent on brand name
- Subtitle: 15px/400, max-width 380px, color `textMid`
- Feature pills: 3 rounded badges — "100% Private", "Local AI", "Fast & Offline" with lock/cpu/zap icons
- CTA: Purple button "Get started →", 14px/700, `boxShadow: 0 4px 20px rgba(124,58,237,0.35)`
- Footer note: "No credit card required · Free during beta"

#### Step 2 — Profile
- Avatar color picker: 8 colored circles (36px), selected state = 3px border + scale(1.15)
- Name fields: First + Last in a 2-col row
- Role selector: pill buttons (wrap), single select
- Roles: Developer, Writer, Researcher, Legal, Compliance, Security, Product Manager, Other

#### Step 3 — Workspace
- Type selector: 2 cards (Personal / Team), full border highlight on selection
- Workspace name input
- Description textarea (2 rows, optional)

#### Step 4 — Invite Team
- Privacy notice: green banner with lock icon
- Dynamic email inputs (add up to 4), remove button per row
- "Add another" dashed button
- Skip button (text only)

#### Step 5 — AI Setup (Ollama)
- Install instructions with terminal code block: dark bg `#111827`, `font-family: monospace`, cyan text
- URL input + "Auto-detect" button — shows spinner while detecting, turns green on success
- Success state: green banner "Ollama found at localhost:11434"
- Model selection: pill buttons with model IDs (monospace font)
- Pull model button with spinner + "Pulling modelname…" state
- Success: "Model ready — you're all set!" in green

**Navigation:**
- Back/Continue buttons, disabled state when required fields empty
- Progress bar: thin lines (4 segments), filled in accent color
- Step counter: "1 / 4" top right
- Slide transition: translateX(32px) → 0 entering, reverse exiting

---

### 2. Home Dashboard

**Layout:** Full-height flex row — Sidebar (62px collapsed / 228px expanded) + Main column (flex:1)

#### Sidebar
3 states:
1. **Expanded (228px):** User avatar + "Owner / Name", nav labels, workspace tree, settings label
2. **Collapsed (62px):** Icons only
3. **Collapsed + hover tooltip:** Dark pill tooltip `right: calc(100% + 10px)` of icon
4. **Collapsed + folder hover:** White popover card with child items list

**Toggle button:**
- `position: absolute`, `right: -11px`, `top: 12px`
- 22px circle, white bg, 1.5px border, accent chevron icon
- `zIndex: 30`, subtle box-shadow
- Hover: border turns accent, bg turns accentBg

**Nav sections:**
```
MAIN
  Home        (house icon)
  Favorites   (heart icon)
  Welcome     (document icon)
  Personal Notes (folder)
  Alpha Product v.0 (folder, expandable)
    → PRD to Launch
    → Finance (highlighted)
    → API Documentation
    → GTM Strategy
SETTINGS
  Settings    (gear icon) → navigates to Settings screen
BOTTOM
  Help        (question circle)
  Logout Account (exit icon, accent color)
```

**Active state:** accentBg background, accent text color, left border not needed
**Hover state:** surfaceAlt background

#### Top Bar (height: 52px)
- Greeting: "Hi {name}, **what are we write together?**" — 18px, 300/800 weight mix
- Right: Tweaks icon (sliders), Bell with unread dot, Help circle button

#### Search Bar
- Full-width input with purple search icon + mic icon
- Focus ring: `0 0 0 3px accentBg`, border turns accent
- Favorite heart shortcuts (3 toggleable hearts)
- "New Document +" button: accent bg, 700 weight, box-shadow

#### Document Cards (Masonry / Grid / List — switchable)
**Masonry:** CSS `columns: 4`, `column-gap: 12px`
**Grid:** `grid-template-columns: repeat(auto-fill, minmax(210px, 1fr))`, `gap: 12px`
**List:** flex column, single-row cards

**Card anatomy (masonry/grid):**
- Cover area (130px): image placeholder OR solid color (purple shades)
- 3-dot menu: appears on hover, top-right, 24px dark button, opens popover menu
- Title: 13px/600, 2-line clamp
- Tags: accentBg pills with accent text, 10px
- Date: 9.5px uppercase, textMuted
- Avatars: stacked circles (-7px margin), 22px, brand colors
- Progress badge: accent bg, white text, 10px/700
- Favorite heart: toggles red fill
- Hover: translateY(-2px), box-shadow increases

**Tweaks Panel** (bottom-right floating, 256px wide):
- Dark/Light toggle, Layout toggle (Masonry/Grid/List), Density (Compact/Normal/Spacious)
- Opened via Tweaks icon in topbar OR `window.__activate_edit_mode` message

---

### 3. Document Editor

**Layout:** Full-height flex row — Editor area (flex:1) + Context Sidebar (268px, toggleable)

#### Editor Topbar (height: 48px)
- Back to Home button
- Breadcrumb: Workspace › Document title
- Status dot (green "Saved")
- Word count
- Collaborator avatar stack
- "Context" sidebar toggle button
- Bell notification icon
- "✦ AI" button (accent, opens AI panel)

#### Block Editor
- Max-width 720px, centered, `padding: 48px 0 120px`
- Tags + date at top
- Blocks rendered from array, each editable via textarea
- `+` add button appears on focused block (left of block, opacity transition)

**Block types:**
```
h1:     28px/800, letter-spacing -0.02em
h2:     20px/700, letter-spacing -0.01em
h3:     16px/700
p:      15px/400, line-height 1.75, textMid color
bullet: 15px/400 with "•" prefix in accent color
num:    15px/400 with "1." prefix in textMuted
code:   13px monospace, accentBg background, accent text, padding 12px 16px, radius 8px
quote:  15px/400 italic, 3px left border in accent color, paddingLeft 16px
```

**H1 block special treatment:**
- `background: #f3f0ff`, `height: 46px`, `border-radius: 8px`

**Slash commands (`/`):**
- Triggers popup (280px wide) with block type list
- Each item: icon badge (28px, accentBg) + label + hint text
- Filtered by query as user types

**@ Mention:**
- Triggers popup with team member list
- Each member: 26px avatar circle + name + role
- Filtered by query
- Inserts `@Name ` on select

**Floating toolbar (text selection):**
- Dark bar: bg `#1c1c2e`, radius 9px
- B / I / U / S format buttons (28px each)
- "✦ AI" accent button
- Position: fixed above selection via `getBoundingClientRect()`

#### Context Sidebar (268px)
3 tabs: **✦ AI** / **Outline** / **Info**

**AI tab:**
- Quick prompt buttons (full list of 7)
- AI result area with streaming text + cursor blink
- Insert / Retry buttons

**Outline tab:**
- TOC from H1/H2/H3 blocks, indented by level
- Active block highlighted with accent left border
- Click to focus block

**Info tab:**
- Status, Progress, Owner, Workspace, Created, Words, Blocks
- 86% progress bar: gradient `#7c3aed → #a855f7`
- Collaborator list with avatars

---

### 4. Notifications Panel

**Layout:** `position: absolute`, right-side slide-in panel (360px wide, full height), `zIndex: 400`

**Header:**
- "Notifications" title + unread count badge
- "Mark all read" button
- All / Unread filter tabs

**Notification item:**
- 36px avatar with 18px type badge (bottom-right)
- Types: edit (doc icon), mention (user icon), ai (zap icon), invite (users icon), comment (doc icon)
- Member name bold + action detail
- Document name with doc icon
- Role label (colored) + timestamp + unread dot
- Unread items: accentBg tinted background + 3px left border in accent

**Team Online section (footer):**
- Horizontal member pills: 22px avatar + first name + green online dot

**Animation:** `slidePanel` — translateX(100%) → 0

---

### 5. Settings Screen

**Layout:** Full-height flex row — Left nav (220px) + Main content (flex:1, scrollable, 40px padding)

#### Left Nav
- Back button
- "Settings" heading 16px/800
- Nav items: Profile, AI & Models, Workspace, Members, Security
- Active: accentBg bg + accent text + accent icon
- Footer: Ollama status pill (Running/Checking/Offline with pulsing dot + active model name)

#### Profile Section
- Avatar preview (60px circle) with initials + role + email
- Color picker row (6 colors, 20px circles)
- First/Last name inputs
- Role pill selector

#### AI & Models Section
**Connection card:**
- URL input + "Re-check" button
- Status banner: green/yellow/red bg depending on state
- Text: "Ollama is running · localhost:11434"

**Parameters card:**
- Temperature: range 0–2, step 0.1, default 0.7
- Max Tokens: range 256–8192, step 256, default 2048
- Context Window: range 2048–32768, step 2048, default 8192
- Each: label + current value (accent color) + range input + hint text

**Model Library card:**
- Each model: ID (monospace/700) + size + speed badge + action buttons
- Active model: accentBg bg + accent border + "Active" badge
- Installed: "Set active" + "Remove" buttons
- Not installed: "Pull" button (accent bg)
- Pulling state: spinner + "Pulling…"

#### Workspace Section
- Name + Description inputs
- Toggle switches: Auto-save, Version history, AI suggestions
- Danger Zone: red bordered card, "Delete workspace" button

#### Members Section
- Member list: avatar + name (you) + role + role `<select>` dropdown
- "Invite" button top right

#### Security Section
- Green "Local-only processing" banner
- Privacy toggles: Local-only mode (on), Telemetry, Crash reports, Analytics
- Audit log: last 4 actions with dot timeline

---

## Interactions & Animations

| Animation       | Properties                              | Duration / Easing                          |
|-----------------|-----------------------------------------|--------------------------------------------|
| fadeUp          | opacity + translateY(16px→0)            | 0.3–0.5s ease                              |
| slideR          | opacity + translateX(32px→0)            | 0.2–0.3s ease                              |
| slideL          | opacity + translateX(-32px→0)           | 0.3s ease                                  |
| slidePanel      | translateX(100%→0)                      | 0.25s cubic-bezier(0.4,0,0.2,1)            |
| popIn           | opacity + scale(0.94→1) + translateY    | 0.15s ease                                 |
| spin            | rotate 360°                             | 0.8s linear infinite                       |
| pulse           | opacity 1→0.4→1                         | 1s infinite                                |
| orbFloat        | translateY + translateX gentle drift    | 6s ease-in-out infinite                    |
| Sidebar expand  | width + min-width                       | 0.25s cubic-bezier(0.4,0,0.2,1)            |
| Card hover      | translateY(-2px) + box-shadow increase  | 0.2s                                       |
| Button hover    | brightness(1.1) + translateY(-1px)      | 0.2s                                       |

---

## State Management

### App-level
```
screen:      "onboarding" | "home" | "settings"
profileData: { profile, workspace, invite, ai }
openDoc:     Document | null
darkMode:    boolean
```

### Home
```
sidebarCollapsed: boolean (default: true)
cards:            Card[]
showNewDoc:       boolean
showNotifs:       boolean
showTweaks:       boolean
tweaks:           { darkMode, layout: "masonry"|"grid"|"list", density: "compact"|"normal"|"spacious" }
```

### Editor
```
blocks:       Block[]  // { id, type, text }
focused:      block id
showSlash:    boolean
slashQ:       string
showMention:  boolean
mentionQ:     string
toolbar:      { x, y } | null
aiPanel:      boolean
aiLoading:    boolean
aiResult:     string
sidebarOpen:  boolean
sidebarTab:   "ai" | "toc" | "info"
showNotifs:   boolean
```

---

## Assets & Icons

All icons are SVG path strings (Lucide-style, 24×24 viewBox, strokeLinecap round):
- home, heart, doc, folder, gear, help, logout, bell, search, mic
- chevronD, chevronR, chevronL, more, plus, x, check
- wifi, cpu, user, users, mail, zap, lock, eye, moon, sun
- grid, list, layout, sliders, arrowR, arrowL

No external icon library is required — all icons are inline SVG paths in the prototype. In production, use Lucide React or Heroicons.

**Fonts:** Inter via Google Fonts — weights 300, 400, 500, 600, 700, 800.

---

## Files

```
design_handoff_writeopia_beta/
├── README.md                  ← This file
└── Writeopia Beta.html        ← Full interactive prototype (single file)
```

Open `Writeopia Beta.html` in any modern browser to interact with the full prototype. Complete the onboarding to reach the home screen; click any card to open the editor; click Settings in the sidebar to open settings.

---

## Implementation Notes for Claude Code

1. **Component library:** Build as React components. Recommended: Next.js App Router + Tailwind CSS + shadcn/ui as a base.
2. **Sidebar:** The toggle button must protrude 11px outside the sidebar (`position:absolute, right:-11px`). Sidebar root must NOT have `overflow:hidden` — only the nav scroll area should.
3. **Tweaks/dark mode:** Global theme should be a React context. The `LIGHT` / `DARK` token objects in the prototype are a good starting point for a theme provider.
4. **AI streaming:** Use `fetch` with `ReadableStream` to stream Ollama responses. The prototype simulates this with `setInterval`.
5. **Block editor:** Consider using a library like TipTap or BlockNote for the production editor, using the prototype as a visual spec.
6. **Ollama integration:** Base URL from settings, use `/api/tags` to list models, `/api/pull` to download, `/api/generate` or `/api/chat` for inference.
