# GPX Track Editor

A powerful, web-based GPX file editor for simplifying, editing, splitting, and joining GPS tracks. Perfect for cleaning up recorded tracks from apps like GeoTracker before sharing or analyzing.

🔗 **Live App**: [https://asg49.github.io/GPX-Editor/](https://asg49.github.io/GPX-Editor/)

![GPX Editor Screenshot](https://img.shields.io/badge/version-5.69-blue) ![License](https://img.shields.io/badge/license-MIT-green)

## Features

### ⚡ Performance
- **Instant load** for massive files (tested with 520,000+ points)
- **Smart lazy-loading** - markers appear on-demand when you zoom in
- **Responsive zoom** - even huge tracks feel snappy
- Handles extreme data efficiently without freezing

### 📉 Track Simplification
- **Douglas-Peucker algorithm** for intelligent point reduction
- **Manual simplification** at any percentage (1-95%) - NO auto-simplification
- **Restore Original** feature to undo simplification instantly
- User controls when and how much to simplify
- Perfect for compression without quality loss

### ✏️ Track Editing
- **Visual point manipulation** - drag points to adjust your route
- **Add points** - tap on the track line to insert new waypoints
- **Delete points** - long-press (2.6s) on any point
- Real-time preview of all edits
- Works smoothly even with 12,000+ points visible

### ✂️ Track Splitting
- **Split mode** - tap any point to divide your track into segments
- **Red X marker** appears at split point, auto-clears after save
- Save individual segments as separate GPX files
- Perfect for extracting specific portions of long recordings

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
- **OpenTopoMap** (new! - topographic contours for hiking)
- Google Satellite
- Google Terrain
- Google Hybrid (satellite + labels)
- Esri World Imagery

### 📊 Navigation Aids
- **Zoom level display** (bottom-left) - real-time zoom indicator
- **Scale bar** (bottom-right) - distance reference at current zoom
- **Fine zoom control** (0.25 increments) - smooth, responsive zooming
- Zoom buttons: + and - for precise control

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

2. **Edit your track**
   - **Drag points**: Touch and drag any red circle to adjust position
   - **Add points**: Tap on the blue/red track line to insert waypoints
   - **Delete points**: Long-press (2.6s) on any point
   - **Change map**: Use layer selector (top-right corner)

3. **Simplify your track**
   - Open menu → Adjust simplification slider (1-95%)
   - Click "Apply Simplification"
   - Check the result
   - Use "Restore Original" if you want to try a different percentage

4. **Manage gaps (joined tracks)**
   - Adjust "Gap Detection" slider (10m - 1,000km)
   - Move up to hide connector lines between segments
   - Move down to see all connections
   - Works in real-time!

5. **Save your work**
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

- **322,000 point file?** Loads in <1 second
- **12,000 points visible?** Still responsive
- Markers appear on-demand when you zoom in (level 8+)
- No performance penalty for massive tracks

## File Format Support

- **Input**: `.gpx` files (GPX 1.0 and 1.1)
- **Output**: `.gpx` files with all original metadata preserved
- **Multi-track**: Properly handles `<trk>` elements without connector lines
- **File System API**: You choose where to save files

## Performance

- **Small tracks** (<1,000 points): Instant
- **Medium tracks** (1K-50K points): Instant load, markers on-demand
- **Large tracks** (50K-500K points): <5 seconds load, lazy markers
- **Extreme tracks** (322K+ points): Instant load, smart lazy-loading
- Optimized for all devices including older ones

## Tips & Best Practices

### For Best Results

1. **Start conservative with simplification** (5-10%) and increase as needed
2. **Use OpenTopoMap** for hiking - shows elevation contours
3. **Adjust gap threshold** based on your data type:
   - Hiking: 100m-1km (tracks are continuous)
   - GPS logs: 1km-10km (short gaps between session starts)
   - Flight data: 10km+ (large gaps between flight segments)
4. **Zoom in to see points** - markers appear at higher zoom levels
5. **Check zoom level** - display shows current zoom (bottom-left)

### Common Workflows

**Cleaning a recorded hike:**
1. Load track (no auto-simplification!)
2. Set slider to 10%
3. Click "Apply Simplification"
4. Review result with OpenTopoMap background
5. Save as `_X.gpx`

**Joining multiple daily hikes into one trip:**
1. Load multiple GPX files at once (2+ = auto-join!)
2. Adjust gap threshold (200m-1km) to break connector lines
3. Review the joined track
4. Save as trip file

**Extracting sections from a long track:**
1. Load track
2. Enable "✂️ Split Mode"
3. Tap points to split
4. Save → get separate files for each section

**Handling flight data (large gaps):**
1. Load multiple flight segments
2. Set gap threshold slider to 4-5 (100km+)
3. No connector lines across flight segments
4. Save joined file

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
- **Lazy Loading**: Markers load on-demand at zoom 8+
- **No server required**: Runs entirely in your browser
- **Privacy**: All processing happens locally - no data uploaded
- **File System API**: Native browser file picker for save locations

## Changelog

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

*Tested with files ranging from 100 points to 322,000 points. Handles Antarctic Peninsula to Puerto Montt journeys like a champ!*
