# GPX Track Editor

A powerful, web-based GPX file editor for simplifying, editing, splitting, and joining GPS tracks. Perfect for cleaning up recorded tracks from apps like GeoTracker before sharing or analyzing.

🔗 **Live App**: [https://asg49.github.io/GPX-Editor/](https://asg49.github.io/GPX-Editor/)

![GPX Editor Screenshot](https://img.shields.io/badge/version-5.83-blue) ![License](https://img.shields.io/badge/license-MIT-green)

## Features

### ⚡ Performance
- **Fast load** for massive files (tested with 500,000+ points in 120MB+ GPX files - loads in several seconds)
- **Smart lazy-loading** - markers appear on-demand based on zoom level AND manual toggle
- **Responsive zoom** - even huge tracks feel snappy
- Handles extreme data efficiently without freezing

### 📉 Track Simplification
- **Douglas-Peucker algorithm** for intelligent point reduction
- **Manual simplification** at any percentage (1-95%) - NO auto-simplification
- **Restore Original** feature to undo simplification instantly
- User controls when and how much to simplify
- Perfect for compression without quality loss
- Respects marker visibility settings during simplification

### 📍 Points Visibility (NEW!)
- **Manual toggle** - Click "● Points ON/OFF" button (bottom-left) to show/hide markers
- **Automatic lazy-loading** - Markers auto-appear when zoomed in high enough
  - Large files (5K+ points): Auto-load at zoom level 8+
  - Medium files (1K-5K points): Auto-load at zoom level 9+
- **Clean default** - No markers on initial load (just blue track line)
- **Red markers** - Appear when shown, making them easy to spot
- **Marker colors**:
  - 🔴 **Red** - Normal mode (markers enabled)
  - 🟠 **Orange** - Split mode (indicates split is active)
  - 🔴 **Red** - Delete mode (indicates delete is active)

### ✏️ Track Editing
- **Visual point manipulation** - drag points to adjust your route
- **Add points** - tap on the track line to insert new waypoints
- **Delete points** - long-press (2.6s) on any point (creates red X marks)
- Real-time preview of all edits
- Works smoothly even with 12,000+ points visible

### ✂️ Track Splitting
- **Split mode** - tap any point to divide your track into segments
- **Red X marker** appears at split point, auto-clears after save
- Save individual segments as separate GPX files
- Perfect for extracting specific portions of long recordings
- Split markers automatically cleaned up during operations

### 🔗 Track Joining
- **Smart multi-file selection** - select 2+ files = auto-join!
- Select 1 file = load normally; select multiple = automatically join
- Combine separate tracks into a single route
- Maintains all metadata and timestamps

### 🌐 Gap Detection (Logarithmic)
- **Prevent connector lines** in joined tracks
- **Gap threshold slider** (10m - 1,000km on logarithmic scale)
- Automatically breaks lines at gaps larger than threshold
- Perfect for flight data and multi-segment recordings
- Adjust slider to hide/show connectors as needed

### 🗺️ Multiple Map Layers
- OpenStreetMap
- **OpenTopoMap** (topographic contours for hiking)
- Google Satellite
- Google Terrain
- Google Hybrid (satellite + labels)
- Esri World Imagery

### 📊 Navigation Aids
- **Zoom level display** (bottom-left) - real-time zoom indicator
- **Scale bar** (bottom-right) - distance reference at current zoom
- **Fine zoom control** (0.25 increments) - smooth, responsive zooming
- Zoom buttons: + and - for precise control
- **Points toggle button** (bottom-left) - Show/hide markers on demand

### 🗺️ Multi-Track Support
- **No connector lines** between separate `<trk>` elements
- Each track renders as independent segments
- Perfect for Google My Maps imports and complex GPX files
- Clean visualization even with dozens of tracks

### 📱 Mobile-Optimized
- Responsive design for phones and tablets
- Touch-friendly controls
- Compact header (minimal screen waste)
- Works offline after first load

## Usage

### Getting Started

1. **Load a GPX file**
   - Click the menu button (☰) in the top-right corner
   - Tap "Load GPX File"
   - Select your GPX file(s) from your device
   - **Multiple files?** They automatically join!

2. **View track points (markers)**
   - **Initial load**: You see only the blue track line (clean, minimal view)
   - **Show markers**: Click the "● Points OFF" button (bottom-left) → changes to "● Points ON"
   - **Hide markers**: Click the "● Points ON" button → changes to "● Points OFF"
   - **Auto-load**: Zoom in high enough and markers appear automatically (even if toggle is OFF)
   - **Marker colors**:
     - 🔴 Red = Normal mode (points visible)
     - 🟠 Orange = Split mode (track splitting)
     - 🔴 Red = Delete mode (point deletion)

3. **Edit your track**
   - **Drag points**: Touch and drag any red circle to adjust position
   - **Add points**: Tap on the blue/red track line to insert waypoints
   - **Delete points**: Long-press (2.6s) on any point (creates red X marker)
   - **Change map**: Use layer selector (top-right corner)

4. **Simplify your track**
   - Open menu → Adjust simplification slider (1-95%)
   - Click "Apply Simplification"
   - Check the result
   - Use "Restore Original" if you want to try a different percentage
   - **Note**: Simplification respects your marker visibility setting

5. **Manage gaps (joined tracks)**
   - Adjust "Gap Detection" slider (10m - 1,000km)
   - Move up to hide connector lines between segments
   - Move down to see all connections
   - Works in real-time!

6. **Save your work**
   - Click "Save GPX" button in the menu
   - Browser's file picker lets you choose save location
   - Files save with `_X` suffix to indicate editing
   - Original files remain unchanged

### Advanced Features

#### Splitting Tracks

1. Click menu → Enable "✂️ Split Mode"
2. Tap on any point where you want to split
3. Red X appears at split point
4. Click "Save GPX" when ready
5. Get TWO separate GPX files automatically
6. Red X clears after save

#### Joining Tracks

**Method 1 (Automatic):**
1. Click menu → "Load GPX File"
2. Select 2+ files at once (Ctrl+Click or Shift+Click)
3. App automatically joins them!

**Method 2 (Explicit):**
1. Click menu → "Load Multiple Files (auto-joins)"
2. Select 2+ files
3. Click "Join All Tracks"

#### Handling Large Files

- **500,000+ point file (120MB+)?** Loads in several seconds with full responsiveness
- **12,000 points visible?** Still responsive at high zoom
- Markers appear on-demand when you zoom in (level 8+) or toggle manually
- No performance penalty for massive tracks after initial load

## File Format Support

- **Input**: `.gpx` files (GPX 1.0 and 1.1)
- **Output**: `.gpx` files with all original metadata preserved
- **Multi-track**: Properly handles `<trk>` elements without connector lines
- **File System API**: You choose where to save files

## Performance

- **Small tracks** (<1,000 points): Instant
- **Medium tracks** (1K-50K points): <1 second load, markers on-demand
- **Large tracks** (50K-500K points): 2-5 seconds load, lazy markers
- **Extreme tracks** (500K+ points in 120MB+ files): Several seconds load, smart lazy-loading
- Optimized for all devices including older ones

## Tips & Best Practices

### For Best Results

1. **Start with clean view** - Load track with markers OFF for clean blue line
2. **Toggle markers when needed** - Click "● Points ON" only when you need to edit/inspect points
3. **Use high zoom to auto-load markers** - Zoom in to level 8+ for instant marker loading
4. **Start conservative with simplification** (5-10%) and increase as needed
5. **Use OpenTopoMap** for hiking - shows elevation contours
6. **Adjust gap threshold** based on your data type:
   - Hiking: 100m-1km (tracks are continuous)
   - GPS logs: 1km-10km (short gaps between session starts)
   - Flight data: 10km+ (large gaps between flight segments)
7. **Check zoom level** - display shows current zoom (bottom-left)

### Understanding Marker Visibility

**Default Behavior:**
- Load file → No markers visible (just blue track)
- Provides clean, minimal interface by default
- Perfect for viewing long tracks without visual clutter

**How to Show Markers:**
1. **Manual toggle**: Click "● Points OFF" button (bottom-left) to enable
2. **Auto-load**: Zoom in high enough (level 8+ for large files, 9+ for medium)
3. **Both work**: Markers stay visible if either condition is true

**Marker Color Meanings:**
- 🔴 **Red circles**: Normal mode (markers visible, edit points)
- 🟠 **Orange circles**: Split mode active (tap to split track)
- 🔴 **Red X marks**: Delete mode (long-press deletes points)

### Common Workflows

**Cleaning a recorded hike:**
1. Load track (markers OFF by default)
2. Click "● Points ON" to see all markers if needed
3. Set slider to 10%
4. Click "Apply Simplification"
5. Review result with OpenTopoMap background
6. Toggle markers OFF to see clean track
7. Save as `_X.gpx`

**Joining multiple daily hikes into one trip:**
1. Load multiple GPX files at once (2+ = auto-join!)
2. Adjust gap threshold (200m-1km) to break connector lines
3. Review the joined track (markers OFF for clean view)
4. Toggle markers ON if you need to inspect specific points
5. Save as trip file

**Extracting sections from a long track:**
1. Load track (markers OFF)
2. Enable "✂️ Split Mode"
3. Toggle "● Points ON" to see markers
4. Tap points to split
5. Save → get separate files for each section

**Handling flight data (large gaps):**
1. Load multiple flight segments
2. Set gap threshold slider to 4-5 (100km+)
3. Toggle markers OFF for clean visualization
4. No connector lines across flight segments
5. Save joined file

## Map Controls

- **+ / - buttons** (left side): Zoom in/out (0.25 increments)
- **Layer control** (top-right): Switch map backgrounds
- **Zoom display** (bottom-left): Current zoom level
- **Scale bar** (bottom-right): Distance reference
- **Menu** (☰): All functions and settings

## Browser Support

- Chrome/Edge (recommended)
- Safari (iOS/macOS)
- Firefox
- Any modern browser with JavaScript enabled

## Technical Details

- **Algorithm**: Douglas-Peucker line simplification
- **Mapping**: Leaflet.js 1.9.4
- **Gap Detection**: Logarithmic scale (10^x meters)
- **Lazy Loading**: Intelligent marker loading based on:
  - Zoom level (8+ for 5K+ point files, 9+ for 1K-5K)
  - User toggle (manual "Points ON/OFF" button)
  - Markers appear when EITHER condition is true
- **Marker Colors**: Dynamic based on mode (Red normal, Orange split, Red delete)
- **No server required**: Runs entirely in your browser
- **Privacy**: All processing happens locally - no data uploaded
- **File System API**: Native browser file picker for save locations
- **Error Handling**: Robust cleanup of split/deletion markers on all operations
- **Performance**: Handles 320K+ point files with instant load and responsive interaction

## Recent Improvements (v5.70-5.83)

✅ **Marker Visibility**
- Added Points toggle button for manual control
- Intelligent lazy-loading respects zoom levels
- Clean default (no markers on load)

✅ **Code Quality**
- Professional code audit (v5.75)
- Robust marker cleanup functions
- Error handling for malformed GPX files
- Extracted magic numbers to named constants

✅ **Bug Fixes**
- Fixed unconditional marker creation after simplification (v5.83)
- Fixed hardcoded red marker color (v5.81)
- Fixed marker persistence on file clear (v5.76)
- Fixed markers reappearing after zoom (v5.77)
- Fixed split/deletion marker cleanup (v5.78-v5.80)

✅ **User Experience**
- Marker colors now indicate mode (orange for split, red for delete)
- No unwanted red markers appearing unexpectedly
- Simplification respects marker visibility settings
- Toggle button works reliably across all operations

## Changelog

### v5.83 (2026-06-14)
- **CRITICAL**: Fixed unconditional marker creation after simplification
- applySimplify() and restoreOriginal() now respect visibility settings
- Markers only appear when user toggles ON or zoom is high enough
- Tested with 120MB+ files - no unwanted red markers!

### v5.82 (2026-06-14)
- Changed default marker color back to RED (visible indicator)
- Markers appear only on toggle or at high zoom (lazy-load)
- Design: Blue line always, red markers on-demand

### v5.81 (2026-06-14)
- **CRITICAL**: Fixed hardcoded red marker color in createMarker()
- Markers now use dynamic color based on mode
- Normal mode: RED, Split mode: ORANGE, Delete mode: RED

### v5.80 (2026-06-14)
- Clear both split markers AND deletion markers before operations
- Added safety cleanup in zoom handler

### v5.79 (2026-06-14)
- Fixed marker flicker during simplification
- Split marker cleanup moved outside setTimeout

### v5.78 (2026-06-14)
- Clear split markers before simplification
- Prevents red X marks from appearing after simplification

### v5.77 (2026-06-14)
- Fixed markers reappearing after zoom on cleared files
- Added explicit empty check in zoomend handler

### v5.76 (2026-06-14)
- Fixed markers persisting after file clear
- Added forceClearMarkers() function

### v5.75 (2026-06-14)
- Professional code audit completed
- Removed unused variables, extracted magic numbers to constants
- Added try-catch to parseGPX(), file size validation

### v5.70-v5.74 (2026-06-14)
- Added points visibility toggle button
- Fixed toggle button variable scoping bug
- Robust split marker cleanup, zoom handler safety checks

### v5.69 (2026-06-13)
- **MAJOR**: Smart multi-file loading (2+ files = auto-join)
- **MAJOR**: Logarithmic gap threshold slider (10m - 1,000km)
- Fixed "kmm" typo in gap threshold display
- Gap detection works for ALL tracks (not just multi-track files)
- Auto-simplification REMOVED - user controls when to simplify
- Added "Restore Original" button for undo
- File System Access API for save location control
- Header and UI optimizations

### v5.68
- Logarithmic gap threshold slider implementation
- Automatic unit conversion (m/km) for display

### v5.67
- No connector lines in joined tracks via gap detection
- Gap threshold applies to all track rendering

### v5.66
- Smart multi-file loading (auto-join)
- Multi-select on load input

### v5.65
- Removed auto-simplification on load
- User controls simplification manually

### v5.64
- Restore Original button
- Emergency save button removed

### v5.61
- OpenTopoMap added to map layers
- Zoom level display + scale bar

### v5.48-5.60
- Lazy marker loading for large files
- Performance optimizations
- Multi-track rendering fixes

### v5.45
- Initial major release with core features

## License

MIT License - see [LICENSE](LICENSE) file for details

## Author

**Tony Gozdz** © 2026  
Battery R&D Engineer  
Serious GPX Geek 🗺️

## Contributing

This is a personal project, but feedback is welcome! Open an issue on GitHub.

## Support

For issues or questions:
1. Check the **About** section in the app menu for tips
2. Open an issue on GitHub
3. Include browser/device info and problem description

---

**Made with ❤️ for outdoor enthusiasts, GPS data nerds, and anyone who records interesting tracks**

*Tested with files ranging from 100 points to 500,000+ points (120MB+ GPX files). Handles massive tracks efficiently with several-second load times for extreme files.*
