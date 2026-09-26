# Pdfy — Streamlined Single-Bar & Clean Card UI Plan

This update eliminates all repeated and redundant buttons across the header, toolbar, bottom bar, and individual file cards so **Pdfy** feels effortless, spacious, and clutter-free on every device.

## User Review & Critical Decisions

> [!IMPORTANT]
> Both layout simplifications have been confirmed to eliminate duplicate controls:

- **Confirmed Decision 1 (Single Action Bar Only)**: Removed duplicate `Add Files`, `Split Pages`, `Options`, `Clear`, and `Merge PDF` buttons that previously appeared across the top header, middle toolbar, and bottom dock. The top bar is now a clean brand header (`Pdfy`), and all document actions live in **one unified action bar**.
- **Confirmed Decision 2 (Minimal File Cards)**: Simplified every file card to show only the **sequence number badge**, **thumbnail** (tap to preview), **Rotate** button, and **Remove** button—removing extra `<`, `>`, `Duplicate`, `View`, and inline inputs from cards.

---

## 1. Overview & Core Concept

- **What It Does**: Provides a zero-clutter PDF and image merger where every action appears once in a predictable location.
- **Target Audience**: Everyday users on phones, tablets, and desktops who want an iLovePDF-style one-click experience without repeated toolbars or crowded card buttons.
- **Key Value**: Zero duplicate buttons, faster visual scanning, and smooth drag-and-drop rearranging.

---

## 2. User Experience & Visual Design

- **Key User Flows**:
  1. **Landing Screen (Zero Files)**: Clean top brand bar (`Pdfy`), centered upload card (`Select PDF or Image Files`), and minimal developer footer.
  2. **Active Workspace (1+ Files)**:
     - **Clean Brand Header**: Shows `Pdfy` on the left and live file/page count summary (`3 files · 6 pages`) on the right—no duplicate action buttons.
     - **Neat Document Grid**: Each card contains only the sequence number (`1`, `2`, `3`), a top-right **Remove (`✕`)** button, a rotatable thumbnail (click/tap thumbnail to open full preview), the truncated filename, and a single **Rotate** button.
     - **Single Unified Action Bar**: One pinned bottom bar containing `+ Add`, `Split PDFs` (shown only when multi-page PDFs are present), `Options`, `Clear`, and the primary `Merge PDF` button.
- **Visual Identity & Theme**:
  - *Aesthetic Direction*: Minimal monochrome slate and crisp white.
  - *Color Palette*: `#F8FAFC` canvas, `#FFFFFF` cards and action bar, `#0F172A` primary buttons and typography, `#64748B` muted metadata, `#E2E8F0` hairline borders.
  - *Typography*: `Plus Jakarta Sans` for UI labels and headings paired with `JetBrains Mono` (`tabular-nums`) for sequence numbers, page counts, and file sizes.

---

## 3. Key Product Decisions & Trade-Offs

- **Decision 1: Consolidating 3 Bars into 1 Unified Action Bar**
  - *Chosen Approach*: Keep all global actions (`+ Add`, `Split PDFs`, `Options`, `Clear`, `Merge PDF`) in a single bottom action bar while keeping the top header strictly for brand identity and live document count.
  - *Why*: Previously, `Add Files`, `Options`, `Split`, and `Merge` were repeated across the top header, workspace toolbar, and bottom bar, creating visual noise.
- **Decision 2: Stripping Card Controls Down to Essentials**
  - *Chosen Approach*: Show only the sequence number, Remove (`✕`), thumbnail (click to preview), and Rotate (`90°`) on each card.
  - *Why*: Drag-and-drop handles reordering naturally, and clicking the thumbnail opens the preview modal, eliminating the need for 6 separate buttons on every card.

---

## 4. Technical Architecture & Data Strategy *(Technical Reference)*

```
┌───────────────────────────────────────────────────────────────────┐
│                     Clean Top Brand Header                        │
│  [ Pdfy ]                                 [ 3 files · 6 pages ]   │
└───────────────────────────────────────────────────────────────────┘
                                  │
                                  ▼
┌───────────────────────────────────────────────────────────────────┐
│                     Main Viewport (Single State)                  │
│  ┌─────────────────────────────┐  ┌─────────────────────────────┐ │
│  │ State A: Empty Upload Card  │  │ State B: Clean Card Grid    │ │
│  │ • Centered Dropzone         │  │ • [#] Badge + [✕] Remove    │ │
│  │ • Select Files CTA          │  │ • Thumbnail (Tap = Preview) │ │
│  └─────────────────────────────┘  │ • Filename + [Rotate 90°]   │ │
│                                   └─────────────────────────────┘ │
└───────────────────────────────────────────────────────────────────┘
                                  │
                                  ▼
┌───────────────────────────────────────────────────────────────────┐
│                  Single Unified Bottom Action Bar                 │
│  [ + Add ]   [ Split PDFs ]   [ Options ]   [ Clear ]  [Merge PDF]│
└───────────────────────────────────────────────────────────────────┘
```

- **Interactive Component & State Mapping**:
  - **Card Dragging (`SortableJS`)**: Dragging any card updates sequence badges (`1`, `2`, `3`...) in real time without ghost/clone numbering glitches.
  - **Card Thumbnail Tap**: Opens the full-resolution page preview modal with Previous/Next page navigation.
  - **Card Rotate Button**: Rotates that item `90°` clockwise and updates the thumbnail transform immediately.
  - **Card Remove Button (`✕`)**: Removes the item and recalculates sequence numbers and page counts.
  - **Single Bottom Action Bar**: Houses the only instances of `+ Add`, conditional `Split PDFs`, `Options` (opens the settings modal for filename, page size, margin, page numbers, and watermark), `Clear`, and `Merge PDF`.
