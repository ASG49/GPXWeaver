# GPXWeaver

A powerful, web-based GPX track editor for simplifying, editing, splitting, and joining GPS tracks. Perfect for cleaning up recorded tracks from apps like GeoTracker before sharing or analyzing.

🔗 **Live App**: [https://asg49.github.io/GPXWeaver/](https://asg49.github.io/GPXWeaver/)

![GPXWeaver](https://img.shields.io/badge/version-7.0-blue) ![License](https://img.shields.io/badge/license-MIT-green)

---

## Features

### ⚡ Performance
- **Fast load** for massive files — tested with 500,000+ points in 120MB+ GPX files
- **Toggle-only marker visibility** — no automatic recalculation on zoom, fast zooming at any scale
- **Clean default** — only the track line is shown on load; markers appear only when you ask for them

### 📉 Track Simplification
- **Douglas-Peucker algorithm** for intelligent point reduction
- **Manual simplification** at any percentage (1–95%)
- **Restore Original** restores the pre-simplify state — including all manual edits made before simplifying
- Simplification always works from the **current edited state** — manually added, dragged, or deleted points are never lost

### 📍 Points Visibility
- **Manual toggle only** — "●○ Points OFF / ● Points ON" controls all marker display
- No automatic zoom-based marker loading — zoom freely without performance hits
- **Marker colors**: 🔴 Red (normal/delete mode) · 🟠 Orange (split mode)

### ✏️ Track Editing
- **Drag points** — move any point to adjust position (6 decimal place precision)
- **Add points** — tap the track line to insert new waypoints with interpolated ele, time, speed, and course
- **Delete points** — long-press (2.6s) on any point to mark for deletion
- **Rectangle Selection** — draw a rectangle to bulk-select and delete multiple points (mobile and desktop)
- All edits survive subsequent simplification operations ✓

### ✂️ Track Splitting
- **Split mode** — tap any point to divide the track at that location
- Save individual segments as separate GPX files

### 🔗 Track Joining — Smart Chaining
- **Select 2+ files** and they join automatically in the correct order
- **Auto-detection of file type:**
  - **GeoTracker recordings** (have timestamps) → sorted **chronologically** by recording date
  - **Google Maps routes** (no timestamps) → chained by **geographic proximity** of endpoints
- Starting track auto-identified; greedy nearest-neighbor eliminates stray connecting lines
- Browser file selection order and alphabetical filename order are irrelevant

### 🌐 Gap Detection
- **Logarithmic gap threshold slider** (10m – 1,000km)
- Prevents unwanted connector lines between segments
- Adjustable in real time

### 🗺️ Map Layers
- OpenStreetMap · OpenTopoMap · Google Terrain *(default)* · Google Satellite · Google Hybrid · Esri World Imagery

### 📊 Navigation Controls

**Desktop:** Zoom display + Points toggle (bottom-left) · Scale bar (bottom-right) · Layer selector (top-right)

**Mobile:** Zoom display (top-left) · Points toggle (top-right) · Scale bar (bottom-right)

### 💾 File Handling
- **Save filename** uses the actual disk filename, not the internal GPX track name
- Edited files get `_X` suffix (e.g. `MyHike_X.gpx`)
- Current filename shown in header bar; updates to `_X` on first edit
- Saved GPX includes `<metadata>` with:
  - **`<name>`**: the save filename
  - **`<time>`**: the **original recording date** from the first trackpoint — ensures correct chronological sorting in GeoTracker
  - Falls back to current date for timestampless files (Google Maps routes)
- All original `<trkpt>` data preserved: elevation, time, speed, course, extensions
- **Coordinate precision**: always 6 decimal places (~0.11m)
- **GeoTracker extensions** (`<geotracker:meta c="course" s="speed"/>`) preserved and interpolated for added points

### 🔒 Security
- `sanitizeHTML()` on all track name display
- `sanitizeXML()` on all GPX output

### 📱 Mobile-Optimized
- Responsive layout; touch-friendly controls including rectangle selection
- Compact header with current filename

---

## Usage

### Getting Started
1. **Load** — Menu (☰) → Load GPX File → select file(s)
2. **View** — blue track line shown immediately
3. **Show markers** — "●○ Points OFF" → "● Points ON"
4. **Edit** — drag, tap to add, long-press to delete, or rectangle-select to bulk-delete
5. **Simplify** — Menu → adjust slider → Apply Simplification (edits are preserved)
6. **Save** — Menu → Save GPX → saves with `_X` suffix and original recording date

### Joining GeoTracker Recordings
1. Menu → Load GPX File → select all recording files
2. GPXWeaver sorts them chronologically by recording timestamp
3. Join All Tracks → saved file retains original recording date for correct GeoTracker sorting

### Joining Google Maps Routes
1. Generate segments (max 10 waypoints each) → convert with [maptogpx.com](https://maptogpx.com)
2. Menu → Load GPX File → select all segment files
3. GPXWeaver chains them geometrically by endpoint proximity → Join All Tracks

### Edit Then Simplify (Correct Workflow)
1. Load file → simplify at desired % if needed
2. Add/drag/delete points as needed
3. Simplify again if needed — **all manual edits are preserved** ✓
4. Save

---

## File Format

- **Input**: `.gpx` (GPX 1.0 and 1.1)
- **Output**: GPX 1.1, all original `<trkpt>` data preserved
- **Metadata**: filename + original recording date
- **Coordinates**: 6 decimal places
- **Namespaces**: declared at root `<gpx>` level

---

## Technical Details

- **Single HTML file** — no install, works offline after first load
- **Leaflet.js** · **Douglas-Peucker** · **Haversine** distance formula
- **Geometric nearest-neighbor chaining** (Google Maps) · **Chronological sort** (GeoTracker)
- `originalTrackpoints` kept in sync with all manual edits — simplification never loses work
- All event listeners inside `DOMContentLoaded` · XSS protection throughout

---

## Changelog

### v7.0 (2026-07-24) — CRITICAL FIX
- **Manual edits no longer lost after re-simplification**
- Root cause: `applySimplify()` always ran from `originalTrackpoints` (frozen at load time)
- Points added/dragged/deleted only existed in `trackpoints` — second simplify wiped them
- Fix: `applySimplify()` snapshots `trackpoints → originalTrackpoints` before simplifying
- `dragend`, point-add, `deleteSelectedPoints()`, `deleteSegmentAndSplit()` all now sync `originalTrackpoints`
- Restore Original correctly restores post-edit pre-simplify state ✓

### v6.9 (2026-07-24)
- `<metadata><time>` uses first trackpoint timestamp (original recording date)
- GeoTracker chronological sorting preserved in saved files
- Falls back to current date for timestampless files

### v6.8 (2026-07-24)
- `chainTracks()` dispatcher: chronological for GeoTracker, geometric for Google Maps
- `chronologicalSortTracks()` added

### v6.7 (2026-07-23)
- Fixed `maxIncomingDist` initialization (`Infinity` → `-Infinity`)
- Geometric chaining now correctly identifies starting track

### v6.6 (2026-07-23)
- Geometric nearest-neighbor track chaining replaces alphabetical sort
- `haversineDistance()` and `geometricChainTracks()` added

### v6.5 (2026-07-22)
- Gap Detection slider initialized correctly inside `DOMContentLoaded`
- `accent-color` added to both sliders

### v6.3 (2026-07-20)
- `cleanInnerXML()` strips redundant `xmlns` from trkpt innerHTML
- Files now load cleanly in all GPX applications

### v6.2 (2026-07-19)
- All event listeners inside `DOMContentLoaded`
- `<metadata>` block in all saved GPX files
- Coordinate precision fixed to 6 decimal places throughout

### v6.0 (2026-07-15)
- GeoTracker `<geotracker:meta>` extensions parsed, preserved, and interpolated
- Major code audit: XSS sanitization, dead code removal, logic consistency

### v5.99–v5.95 (2026-07-15)
- Full `<trkpt>` innerHTML preserved · filename in header · disk filename on save
- Toggle-only point visibility · all event listeners and security hardened

### v5.94 (2026-06-24)
- Rectangle selection fixed on mobile (`changedTouches`)

### v5.87 (2026-06-18)
- Mobile controls: zoom top-left, toggle top-right, scale bottom-right

---

## License

MIT License — see [LICENSE](LICENSE) for details.

## Author

**Tony Gozdz** © 2026 · Battery R&D Engineer · Serious GPX Geek 🗺️

---

*Tested with files from 100 to 500,000+ points (120MB+ GPX). All operations — drag, add, delete, rectangle select, split, join, simplify — work reliably on mobile and desktop. Manual edits always survive re-simplification.*
