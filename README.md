# GPXWeaver

A powerful, web-based GPX track editor for simplifying, editing, splitting, and joining GPS tracks. Perfect for cleaning up recorded tracks from apps like GeoTracker before sharing or analyzing.

🔗 **Live App**: [https://asg49.github.io/GPXWeaver/](https://asg49.github.io/GPXWeaver/)

![GPXWeaver](https://img.shields.io/badge/version-6.9-blue) ![License](https://img.shields.io/badge/license-MIT-green)

---

## Features

### ⚡ Performance
- **Fast load** for massive files — tested with 500,000+ points in 120MB+ GPX files
- **Toggle-only marker visibility** — no automatic recalculation on zoom, fast zooming at any scale
- **Clean default** — only the track line is shown on load; markers appear only when you ask for them

### 📉 Track Simplification
- **Douglas-Peucker algorithm** for intelligent point reduction
- **Manual simplification** at any percentage (1–95%) — no auto-simplification
- **Restore Original** to undo simplification at any time
- Simplification respects your current marker visibility setting

### 📍 Points Visibility
- **Manual toggle only** — "●○ Points OFF / ● Points ON" button controls all marker display
- No automatic zoom-based marker loading — zoom freely without performance hits
- **Marker colors**: 🔴 Red (normal/delete mode) · 🟠 Orange (split mode)

### ✏️ Track Editing
- **Drag points** — move any point to adjust position (coordinates rounded to 6 decimal places)
- **Add points** — tap the track line to insert new waypoints with interpolated ele, time, speed, and course
- **Delete points** — long-press (2.6s) on any point to mark for deletion
- **Rectangle Selection** — draw a rectangle to bulk-select and delete multiple points (works on mobile and desktop)
- All edits update the track line in real time

### ✂️ Track Splitting
- **Split mode** — tap any point to divide the track at that location
- Save individual segments as separate GPX files
- Split markers auto-clean after save

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
- Adjustable in real time; slider correctly initialized on load

### 🗺️ Map Layers
- OpenStreetMap
- OpenTopoMap (topographic contours)
- Google Terrain *(default)*
- Google Satellite
- Google Hybrid
- Esri World Imagery

### 📊 Navigation Controls

**Desktop:**
- Zoom display + Points toggle — bottom-left
- Scale bar — bottom-right
- Layer selector — top-right

**Mobile:**
- Zoom display — top-left (below +/− buttons)
- Points toggle — top-right
- Scale bar — bottom-right

### 💾 File Handling
- **Save filename** uses the actual disk filename you loaded, not the internal GPX track name
- Edited files get `_X` suffix (e.g. `MyHike_X.gpx`)
- Current filename displayed in header bar; updates to `_X` on first edit
- Saved GPX includes a `<metadata>` block with:
  - **`<name>`**: the save filename
  - **`<time>`**: the **original recording date** from the first trackpoint (not the save date) — ensures correct chronological sorting in GeoTracker
  - Falls back to current date only for Google Maps routes with no timestamps
- All original `<trkpt>` data preserved: elevation, time, speed, course, extensions
- **Coordinate precision**: always 6 decimal places (~0.11m)
- **GeoTracker extensions** (`<geotracker:meta c="course" s="speed"/>`) fully preserved and interpolated for added points

### 🔒 Security
- `sanitizeHTML()` on all track name display
- `sanitizeXML()` on all GPX output
- Protects against malicious GPX files with injected content

### 📱 Mobile-Optimized
- Responsive layout for phones and tablets
- Touch-friendly controls including rectangle selection (`changedTouches` fix for reliable touch-end detection)
- Compact header with current filename displayed

---

## Usage

### Getting Started

1. **Load a GPX file** — Menu (☰) → Load GPX File → select file(s)
   - Select multiple files to auto-chain and join them
2. **View your track** — blue line shown immediately
3. **Show markers** — click "●○ Points OFF" → "● Points ON"
4. **Edit** — drag points, tap line to add, long-press to delete, or rectangle-select to bulk-delete
5. **Simplify** — Menu → adjust slider → Apply Simplification → Restore Original if needed
6. **Save** — Menu → Save GPX → saves with `_X` suffix and original recording date

### Joining Multiple Google Maps Routes
1. Generate route segments in Google Maps (max 10 waypoints each)
2. Convert each to GPX using [maptogpx.com](https://maptogpx.com)
3. Menu → Load GPX File → select all segment files at once
4. GPXWeaver chains them geometrically by endpoint proximity
5. Review the join list → Join All Tracks

### Joining GeoTracker Recordings
1. Menu → Load GPX File → select all recording files at once
2. GPXWeaver sorts them chronologically by recording timestamp
3. Review the join list → Join All Tracks
4. Saved file retains the original recording date for correct GeoTracker sorting

### Rectangle Selection (Bulk Delete)
1. Menu → Enable "Rectangle Select"
2. Draw a rectangle over the points to remove
3. Tap "Delete Selected"

### Splitting a Track
1. Menu → Enable "Split Mode"
2. Tap the split point
3. Save → downloads as separate GPX files

---

## File Format

- **Input**: `.gpx` files (GPX 1.0 and 1.1)
- **Output**: GPX 1.1, all original `<trkpt>` data preserved
- **Metadata**: `<metadata>` block with filename and original recording date
- **Coordinates**: 6 decimal places in all output
- **Namespaces**: GeoTracker and other extension namespaces declared at root `<gpx>` level

---

## Map Controls Summary

| Control | Desktop | Mobile |
|---------|---------|--------|
| Zoom +/− | top-left | top-left |
| Zoom display | bottom-left | top-left |
| Points toggle | bottom-left | top-right |
| Layer selector | top-right | top-right |
| Scale bar | bottom-right | bottom-right |

---

## Technical Details

- **Single HTML file** — no install, works offline after first load
- **Leaflet.js** mapping library
- **Douglas-Peucker** simplification algorithm
- **Haversine** distance formula for accurate geographic calculations
- **Geometric nearest-neighbor chaining** for Google Maps route ordering
- **Chronological sort** for GeoTracker recordings (timestamp-based)
- All event listeners inside `DOMContentLoaded`
- XSS protection throughout

---

## Recent Improvements (v6.0–v6.9)

✅ **v6.9 — Original recording date in GPX metadata**
- `<metadata><time>` now uses first trackpoint timestamp, not today's save date
- GeoTracker sorts files by internal date — saved files now appear in correct position
- Falls back to current date for Google Maps routes (no timestamps)

✅ **v6.8 — Smart track chaining**
- `chainTracks()` dispatcher auto-detects file type:
  - Timestamps present → chronological sort (GeoTracker recordings)
  - No timestamps → geometric nearest-neighbor (Google Maps routes)
- Toast message confirms which method was used

✅ **v6.7 — Geometric chaining bug fix**
- `maxIncomingDist` was initialized to `Infinity` — condition always false
- Starting track was never updated; tracks joined in browser file order
- Fixed: initialized to `-Infinity`; geometric chaining now works correctly

✅ **v6.6 — Geometric track chaining**
- Replaced alphabetical sort with nearest-neighbor geographic chaining
- `haversineDistance()` and `geometricChainTracks()` added
- Eliminates stray connecting lines from wrong join order

✅ **v6.5 — Gap slider initialization**
- Slider thumb now correctly positioned on load (was rendering at far right)
- `accent-color` added for visibility on dark background

✅ **v6.3 — Namespace fix**
- `cleanInnerXML()` strips redundant `xmlns=` injected by browser innerHTML serialization
- Files now load cleanly in all GPX applications

✅ **v6.2 — Event listeners & metadata**
- All event listeners moved inside `DOMContentLoaded`
- `<metadata>` block added to all saved GPX files
- Coordinate precision fixed to 6 decimal places throughout

✅ **v6.0 — GeoTracker data preservation**
- Full `<trkpt>` innerHTML preserved through all edit operations
- `interpolateSpeed()` and `interpolateCourse()` for added points
- Major code audit: XSS sanitization, dead code removal, logic fixes

---

## Changelog

### v6.9 (2026-07-24)
- `<metadata><time>` uses first trackpoint timestamp (original recording date)
- GeoTracker chronological sorting now preserved in saved files
- Fallback to current date for timestampless files (Google Maps routes)
- Applied to all three GPX generators ✓

### v6.8 (2026-07-24)
- `chainTracks()` dispatcher: chronological for GeoTracker, geometric for Google Maps
- `chronologicalSortTracks()` added; sorts by first point timestamp
- Toast confirms join method used

### v6.7 (2026-07-23)
- Fixed `maxIncomingDist` initialization (`Infinity` → `-Infinity`)
- Geometric chaining now correctly identifies starting track ✓

### v6.6 (2026-07-23)
- Geometric nearest-neighbor track chaining replaces alphabetical sort
- `haversineDistance()` and `geometricChainTracks()` added
- 500m endpoint threshold for shared waypoint matching

### v6.5 (2026-07-22)
- Gap Detection slider initialized correctly inside `DOMContentLoaded`
- `accent-color` added to both sliders for dark-background visibility

### v6.4 (2026-07-22)
- Slider accent color styling

### v6.3 (2026-07-20)
- `cleanInnerXML()` strips redundant `xmlns` from trkpt innerHTML
- `xmlns:geotracker` declared at root `<gpx>` element
- Fixed read-back failure for files saved by v6.2

### v6.2 (2026-07-19)
- All event listeners inside `DOMContentLoaded`
- `<metadata>` block in all saved GPX files
- Coordinate precision fixed in `generateGPXForTrack()`
- Duplicate `#header` CSS rule fixed

### v6.1 (2026-07-19)
- Dragged and added point coordinates rounded to 6 decimal places

### v6.0 (2026-07-15)
- GeoTracker `<geotracker:meta>` extensions parsed, preserved, and interpolated
- Major code audit: sanitization, duplicate removal, logic consistency

### v5.99 (2026-07-15)
- Full `<trkpt>` innerHTML preserved through all edits via all three GPX generators

### v5.98 (2026-07-15)
- Filename shown in header bar; updates on edit; cleared on track clear

### v5.97 (2026-07-15)
- Save uses disk filename not internal GPX `<name>` tag

### v5.96 (2026-07-15)
- `sanitizeHTML()` and `sanitizeXML()` applied throughout
- Dead code, duplicate functions, unused constants removed

### v5.95 (2026-07-15)
- Toggle-only point visibility; no auto-zoom recalculation

### v5.94 (2026-06-24)
- Rectangle selection fixed on mobile (`changedTouches`)

### v5.87 (2026-06-18)
- Mobile controls: zoom top-left, toggle top-right, scale bottom-right

---

## License

MIT License — see [LICENSE](LICENSE) file for details.

## Author

**Tony Gozdz** © 2026  
Battery R&D Engineer · Serious GPX Geek 🗺️

---

*Tested with files from 100 to 500,000+ points (120MB+ GPX). All editing operations — drag, add, delete, rectangle select, split, join, simplify — work reliably on both mobile and desktop.*
