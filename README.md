# GPXWeaver

A powerful, web-based GPX track editor for simplifying, editing, splitting, and joining GPS tracks. Perfect for cleaning up recorded tracks from apps like GeoTracker before sharing or analyzing.

🔗 **Live App**: [https://asg49.github.io/GPXWeaver/](https://asg49.github.io/GPXWeaver/)

![GPXWeaver](https://img.shields.io/badge/version-6.2-blue) ![License](https://img.shields.io/badge/license-MIT-green)

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

### 🔗 Track Joining
- **Smart multi-file loading** — select 2+ files and they join automatically
- Select 1 file = load normally; select multiple = auto-join

### 🌐 Gap Detection
- **Logarithmic gap threshold slider** (10m – 1,000km)
- Prevents unwanted connector lines between segments in joined or recorded tracks
- Adjustable in real time

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
- Saved GPX always includes a `<metadata>` block with save filename and UTC timestamp
- All original `<trkpt>` data preserved on save: elevation, time, speed, course, extensions
- **Coordinate precision**: always 6 decimal places (~0.11m — more than sufficient for GPS)
- **GeoTracker extensions** (`<geotracker:meta c="course" s="speed"/>`) fully preserved and interpolated for added points

### 🔒 Security
- HTML sanitization on all track name display (`sanitizeHTML()`)
- XML sanitization on all GPX output (`sanitizeXML()`)
- Protects against malicious GPX files with injected content

### 📱 Mobile-Optimized
- Responsive layout for phones and tablets
- Touch-friendly controls including rectangle selection (fixed `changedTouches` for reliable touch-end detection)
- Compact header with current filename displayed

---

## Usage

### Getting Started

1. **Load a GPX file** — Menu (☰) → Load GPX File → select file(s)
   - Select multiple files to auto-join them
2. **View your track** — blue line shown immediately; no markers until you ask
3. **Show markers** — click "●○ Points OFF" → becomes "● Points ON"
4. **Edit** — drag points, tap line to add, long-press to delete, or draw a rectangle to bulk-delete
5. **Simplify** — Menu → adjust slider → Apply Simplification → Restore Original if needed
6. **Save** — Menu → Save GPX → file saves with `_X` suffix using your original filename

### Rectangle Selection (Bulk Delete)
1. Menu → Enable "Rectangle Select"
2. Draw a rectangle over the points you want to remove
3. Tap "Delete Selected" to remove them all at once

### Splitting a Track
1. Menu → Enable "Split Mode"
2. Tap the point where you want to split
3. Save → downloads as separate GPX files

### Joining Tracks
- **Auto**: Menu → Load GPX File → select 2+ files at once
- **Manual**: Menu → Load Multiple Files → Join All Tracks

### Gap Detection (Joined Tracks)
- Menu → adjust Gap Detection slider
- Increase to hide connector lines between segments
- Works in real time

---

## File Format

- **Input**: `.gpx` files (GPX 1.0 and 1.1)
- **Output**: GPX 1.1, all original `<trkpt>` data preserved (ele, time, speed, course, extensions)
- **Metadata**: `<metadata>` block added to every saved file with name and timestamp
- **Coordinates**: 6 decimal places in all output

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

- **Single HTML file** — no dependencies to install, works offline after first load
- **Leaflet.js** mapping library
- **Douglas-Peucker** simplification algorithm
- **File System Access API** for save location control
- All event listeners properly registered inside `DOMContentLoaded`
- XSS protection on all user-generated content inserted into HTML or XML

---

## Recent Improvements (v5.95–v6.2)

✅ **v6.2 — Code correctness & GPX metadata**
- All event listeners moved inside `DOMContentLoaded` (was causing menu/layer control failures)
- GPX `<metadata>` block (filename + UTC timestamp) added to all saved files
- Coordinate precision fixed to 6 decimal places in all three GPX generators
- CSS header conflict fixed (duplicate `#header` rule with `position: relative` was hiding header)

✅ **v6.1 — Coordinate precision**
- Dragged and added points now stored and output at 6 decimal places (was 15+)

✅ **v6.0 — GeoTracker data preservation**
- Full `<trkpt>` `innerHTML` preserved on load and save (speed, course, extensions, all tags)
- `interpolateSpeed()` and `interpolateCourse()` for added points (with 0°/360° wrap handling)
- Comprehensive code audit: XSS sanitization, dead code removal, duplicate function removed, logic consistency

✅ **v5.99 — trkpt round-tripping**
- All three GPX generators now output `innerXML` verbatim for existing points
- Synthesized points fall back to ele/time only

✅ **v5.98 — Header filename display**
- Current filename shown in header bar (right-aligned, between title and ☰)
- Updates to `_X` suffix on first edit; clears on track clear; hidden in join mode

✅ **v5.97 — Save filename fix**
- Save now uses the actual disk filename, not the internal GPX `<name>` tag
- `markAsEdited()` appends `_X` to the disk filename

✅ **v5.96 — Security & logic audit**
- `sanitizeHTML()` and `sanitizeXML()` added and applied throughout
- Removed duplicate `generateGPXForTrack()`, dead code, unused constants
- All `createMarkers()` calls now respect toggle-only rule

✅ **v5.95 — Toggle-only marker visibility**
- Removed all auto-zoom-based marker display
- `zoomend` handler does safety cleanup only — no marker recalculation
- Fast zooming at any zoom level, any file size

✅ **v5.94 — Rectangle selection mobile fix**
- Root cause: `e.touches` is empty on `touchend` (finger already lifted)
- Fixed `getEventPoint()` to use `e.changedTouches`
- Rectangle selection now works reliably on mobile

✅ **v5.87 — Mobile control layout**
- Zoom at top-left, Points toggle at top-right, scale at bottom-right on mobile
- Desktop unchanged: zoom + toggle at bottom-left

---

## Changelog

### v6.2 (2026-07-19)
- Fixed all event listeners to be inside `DOMContentLoaded` (menu and layer dropdown were broken)
- Added `<metadata>` block (filename + UTC timestamp) to all saved GPX files
- Fixed coordinate precision to 6 decimal places in `generateGPXForTrack()` (was using raw float)
- Fixed CSS duplicate `#header` rule hiding the header bar
- Fixed `deleteSelectedPoints()` to use disk filename for `_X` suffix

### v6.1 (2026-07-19)
- Fixed dragged points: stored at 6 decimal places (was full float precision ~15 digits)
- Fixed added points: stored at 6 decimal places
- Fixed multitrack GPX generators: `toFixed(7)` → `toFixed(6)`

### v6.0 (2026-07-15)
- Parses GeoTracker `<geotracker:meta c="course" s="speed"/>` extensions
- `interpolateSpeed()` and `interpolateCourse()` for added points
- Added points now include interpolated extensions in their `innerXML`
- Major code audit: XSS sanitization, dead code removal, brace/indentation fixes, operator precedence, consistent creator version across all GPX generators

### v5.99 (2026-07-15)
- All `<trkpt>` data preserved through edits via `innerXML` capture on parse
- All three GPX generators output `innerXML` verbatim for existing points

### v5.98 (2026-07-15)
- Filename displayed in header bar (right-aligned, italic, truncates if too long)
- Cleared on track clear; not shown in join mode

### v5.97 (2026-07-15)
- Save uses actual disk filename (not internal GPX track name)
- `markAsEdited()` appends `_X` to disk filename, updates header display

### v5.96 (2026-07-15)
- `sanitizeHTML()` and `sanitizeXML()` added; applied to all track name insertions
- Removed duplicate `generateGPXForTrack()` function
- Removed dead `adjustSimplifyForTarget()`, unused `ZOOM_THRESHOLD` constants, empty stubs
- All `createMarkers()` calls enforce toggle-only rule
- `clearMarkers()` state management fixed
- `clearSelection()` null-check on `getElement()`
- Fixed `percentToTolerance()` indentation, operator precedence in `interactive:` option
- All three GPX generators use consistent `creator="GPXWeaver vX.X"`

### v5.95 (2026-07-15)
- Removed all automatic zoom-based marker visibility
- `zoomend` handler now only does safety cleanup
- Toggle button sole control: "●○ Points OFF" / "● Points ON"
- Fast zooming at any zoom level, no recalculation overhead

### v5.94 (2026-06-24)
- Fixed rectangle selection on mobile (`e.changedTouches` instead of `e.touches`)
- Fixed `clearMarkers()` to always remove markers from map

### v5.87 (2026-06-18)
- Mobile controls: zoom top-left, toggle top-right, scale bottom-right
- Desktop unchanged

### v5.83 (2026-06-14)
- Fixed unconditional marker creation after simplification and restore

### v5.69 (2026-06-13)
- Smart multi-file auto-join
- Logarithmic gap threshold slider (10m–1,000km)
- Restore Original button; auto-simplification removed

### v5.45 and earlier
- Core features: rectangle selection, track splitting/joining, gap detection, Douglas-Peucker simplification, multi-map layers, lazy marker loading

---

## License

MIT License — see [LICENSE](LICENSE) file for details.

## Author

**Tony Gozdz** © 2026  
Battery R&D Engineer · Serious GPX Geek 🗺️

## Support

Open an issue on GitHub with your browser/device info and a description of the problem.

---

*Tested with files from 100 to 500,000+ points (120MB+ GPX). Handles extreme files efficiently. All editing operations — drag, add, delete, rectangle select, split, join, simplify — work reliably on both mobile and desktop.*
