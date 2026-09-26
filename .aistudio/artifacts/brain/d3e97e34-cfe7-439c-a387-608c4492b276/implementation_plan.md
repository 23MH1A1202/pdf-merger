# Pdfy — Minimalist PDF & Image Merger

Redesign the application into **Pdfy**, an ultra-simple, distraction-free PDF and image toolkit inspired by iLovePDF. The interface eliminates technical jargon, explanatory paragraphs, and sample generators in favor of a two-stage flow—a single centered upload screen that transitions into a visual card organizer with a on-demand options popup—crafted in a minimal monochrome slate-and-white palette with developer attribution for **Ambati Lalitha Sagar**.

## User Review & Critical Decisions

> [!IMPORTANT]
> All design preferences from your responses have been locked into this blueprint:

- **Confirmed Decision 1 — On-Demand Options Popup**: Optional PDF settings (page size, margins, page numbers, watermark, custom file name) are hidden inside a clean collapsible popup/drawer triggered only when the user clicks **Options**, keeping the main workspace effortless.
- **Confirmed Decision 2 — Minimal Monochrome Slate & White Theme**: High-contrast `#0F172A` slate actions and typography over `#FFFFFF` and `#F8FAFC` neutral surfaces, avoiding visual noise.
- **Confirmed Decision 3 — Centered Upload Screen (Zero State)**: Before files are selected, the app displays a single centered upload dropzone with a large **Select Files** button—no multi-column dashboards, no long text blocks, and no sample document buttons.
- **Confirmed Decision 4 — Branding & Developer Credits**: Rebranded to **Pdfy** with clean developer links for **Ambati Lalitha Sagar** (`alsagar.tech` and `lalithasagarambati@gmail.com`) in the header and footer.

---

## 1. Overview & Core Concept

- **What It Does**: Lets anyone combine PDFs and photos, reorder pages by dragging or tapping arrows, rotate items, split multi-page PDFs into single pages, and download one combined PDF.
- **Target Audience / Persona**: Everyday users on phones, tablets, and desktops who want an instant, self-explanatory tool that requires zero reading.
- **Key Value**: Kindergarten-level simplicity on the surface, backed by full client-side PDF power (page splitting, custom page selection, rotation, page numbering, and watermarks) tucked neatly behind simple 1-word action buttons.

---

## 2. User Experience & Visual Design

### Key User Flows

1. **Stage 1 — Centered Upload Screen (0 Files)**:
   - Displays a clean centered card with a bold heading (**Merge PDF & Images**), a one-line prompt (**Drop files here or tap below**), and a large **Select Files** button.
   - All sample file generators and instructional paragraphs are completely removed.
2. **Stage 2 — Visual Card Workspace (1+ Files)**:
   - Once files are added, the centered screen smoothly switches to the visual file grid (or compact list view on mobile).
   - Each card shows:
     - Clear order number (`1`, `2`, `3`...) that updates live while dragging.
     - Crisp page preview thumbnail (tap to view larger).
     - Simple 1-tap icon buttons: **Rotate**, **Split Pages** (for multi-page PDFs), **Move Left/Right**, and **Remove**.
3. **Stage 3 — Options Drawer & One-Tap Merge**:
   - A clean bottom bar (and top action on desktop) holds three simple controls: **+ Add More**, **Options** (opens the settings popup for file name, page size, page numbers, or watermark), and **Merge PDF**.
   - Clicking **Merge PDF** downloads the combined file and opens a clean "Ready" modal/banner where users can **Download Again**, **Preview**, or **Start New** without losing their work unless they choose to clear.

### Visual Identity & Theme

- **Aesthetic Direction**: Utilitarian minimalism inspired by iLovePDF—big touch targets, short 1–2 word labels, generous whitespace, and zero technical jargon.
- **Color Palette & Mood**:
  - `--background`: `#F8FAFC` (Soft cool off-white canvas)
  - `--surface`: `#FFFFFF` (Pure white cards, header, and modals)
  - `--primary`: `#0F172A` (Deep slate ink for primary buttons, active states, and sequence badges)
  - `--muted`: `#64748B` (Subtle slate for short labels like `3 Pages`)
  - `--border`: `#E2E8F0` (Clean 1px hairline dividers)
- **Typography & Hierarchy**:
  - **Display & UI**: `Plus Jakarta Sans` (SemiBold/Bold for headings and buttons, Regular/Medium for short labels).
  - **Numbers & Counters**: `JetBrains Mono` with `tabular-nums` for page numbers (`1`, `2`, `3`), file sizes, and loading progress (`0%`–`100%`).
- **Component Styling & Mobile Ergonomics**:
  - Minimum `44×44px` touch targets on mobile controls.
  - Strictly truncated single-line filenames inside cards and inside the loading popup so long filenames never overflow.
  - Aggregate sticky height on mobile stays well below 15% of the viewport height.

---

## 3. Key Product Decisions & Trade-Offs

- **Decision 1 — Progressive Disclosure via Options Modal/Drawer**
  - *Chosen Approach*: Keep page standardization (Original / A4 / Letter), page numbering, and watermark inputs inside a dedicated **Options** modal/drawer rather than an always-visible sidebar.
  - *Why*: Eliminates visual clutter and allows the file cards to use the full width of the screen while keeping advanced formatting 1 tap away.
  - *Alternatives Considered*: Permanent right-hand sidebar (rejected because it crowds the screen and introduces too many form fields upfront).
- **Decision 2 — Direct Page Splitting & Visual Page Picker**
  - *Chosen Approach*: Instead of asking users to type syntax for page ranges, multi-page PDF cards feature a simple **Split Pages** button (to burst the PDF into individual page cards) and a **Pages** button inside the preview modal to toggle pages visually or enter simple ranges.
  - *Why*: Much easier for non-technical users on both phones and desktops.

---

## 4. Technical Architecture & Data Strategy

### Architecture & Component Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                              Pdfy App Shell                             │
│  ┌───────────────────┐   ┌───────────────────────┐   ┌───────────────┐  │
│  │ Brand: "Pdfy"     │   │ Clean Action Links    │   │ Developer     │  │
│  │ (Single Wordmark) │   │ (Clear / Grid / List) │   │ Portfolio CTA │  │
│  └───────────────────┘   └───────────────────────┘   └───────────────┘  │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                 ┌───────────────────┴───────────────────┐
                 ▼ (0 Files)                             ▼ (1+ Files)
┌─────────────────────────────────┐     ┌─────────────────────────────────┐
│   Stage 1: Centered Dropzone    │     │  Stage 2: Sortable Card Canvas  │
│  • Big "Select Files" Button    │     │  • Live Sequence Number Sync    │
│  • Drag & Drop Anywhere Support │     │  • 1-Tap Rotate / Split / Move  │
│  • Zero Clutter / No Samples    │     │  • Tap Thumbnail -> Preview     │
└─────────────────────────────────┘     └────────────────┬────────────────┘
                                                         │
                         ┌───────────────────────────────┼────────────────┐
                         ▼                               ▼                ▼
         ┌──────────────────────────────┐  ┌───────────────────┐  ┌───────────────┐
         │ Collapsible Options Modal    │  │ Page Previewer    │  │ Merge Engine  │
         │ • File Name                  │  │ • High-Res Zoom   │  │ (pdf-lib +    │
         │ • Page Size (Auto/A4/Letter) │  │ • Page Stepper    │  │  pdf.js)      │
         │ • Page Numbers (On/Off)      │  │ • Rotate / Delete │  │ • Instant Save│
         │ • Watermark Text             │  └───────────────────┘  └───────────────┘
         └──────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│  Minimal Footer: Ambati Lalitha Sagar · alsagar.tech · Email Contact    │
└─────────────────────────────────────────────────────────────────────────┘
```

### Data Model & State

- **`workspaceItems` Array**: Stores each uploaded PDF or image in memory (`id`, `name`, `kind`, `arrayBuffer`, `totalPages`, `selectedPages`, `rotation`, `thumbUrl`, `isSinglePageSlice`).
- **`outputSettings` Object**: Stores user-selected options from the collapsible popup (`fileName`, `pageSize`, `margin`, `pageNumbers`, `watermark`).

### Interactive Component & State Mapping

- **Upload & Drag-Anywhere Handler**: Dropping files anywhere on the window or clicking **Select Files** opens the progress popup (with strict single-line filename truncation) and transitions from Stage 1 (Centered Upload) to Stage 2 (Card Grid).
- **Glitch-Free Reordering**: Dragging a card or tapping `<` / `>` immediately recalculates `1, 2, 3...` across all active cards (filtering out Sortable's temporary drag clone) and updates the floating clone badge to match.
- **Options Drawer/Popup**: Clicking **Options** opens a clean modal/bottom-sheet drawer where users can toggle page numbers, pick A4/Letter size, or rename the output PDF.
- **Developer Attribution**: Clean, unboxed links in the footer (and subtle header link) pointing to `https://alsagar.tech` and `mailto:lalithasagarambati@gmail.com` for **Ambati Lalitha Sagar**.
