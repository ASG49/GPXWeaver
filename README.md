# GPX Track Editor

A powerful, web-based GPX file editor for simplifying, editing, splitting, and joining GPS tracks. Perfect for cleaning up recorded tracks from apps like GeoTracker before sharing or analyzing.

🔗 **Live App**: [https://asg49.github.io/GPX-Editor/](https://asg49.github.io/GPX-Editor/)

![GPX Editor Screenshot](https://img.shields.io/badge/version-4.9-blue) ![License](https://img.shields.io/badge/license-MIT-green)

## Features

### 📉 Track Simplification
- **Douglas-Peucker algorithm** for intelligent point reduction
- Adjustable simplification level (1-95%)
- **Auto-simplification** for large files (>5,000 points)
- Handles massive tracks efficiently (tested with 790,000+ points)
- **Restore Original** feature to undo simplification

### ✏️ Track Editing
- **Visual point manipulation** - drag points to adjust your route
- **Add points** - tap on the track line to insert new waypoints
- **Delete points** - long-press (2.6s) on any point
- Real-time preview of all edits
- Automatic filename cleanup (removes doubled dates from GeoTracker exports)

### ✂️ Track Splitting
- **Split mode** - tap any point to divide your track into segments
- Preview all segments before saving
- Save individual segments as separate GPX files
- Perfect for extracting specific portions of long recordings

### 🔗 Track Joining
- **Multi-file selection** - load multiple GPX files at once
- Combine separate tracks into a single route
- Maintains all metadata and timestamps
- Useful for creating continuous tracks from multiple recordings

### 🗺️ Multiple Map Layers
- OpenStreetMap (default)
- Google Satellite
- Google Terrain/Topographic
- Google Hybrid (satellite + labels)
- Esri World Imagery

### 📱 Mobile-Optimized
- Responsive design for phones and tablets
- Touch-friendly controls
- Works offline after first load (PWA-ready)
- Emergency save button (always accessible)

## Usage

### Getting Started

1. **Load a GPX file**
   - Click the menu button (☰) in the top-right corner
   - Tap "Load GPX File"
   - Select your GPX file from your device

2. **Edit your track**
   - **Drag points**: Touch and drag any red circle to adjust position
   - **Add points**: Tap on the blue track line to insert waypoints
   - **Delete points**: Long-press (2.6s) on any point, confirm deletion
   - **Change map layer**: Use the layer control in top-right corner

3. **Simplify your track**
   - Open menu → Adjust the simplification slider (1-95%)
   - Click "Simplify Track"
   - Higher percentage = more aggressive simplification
   - Use "Restore Original" to undo

4. **Save your work**
   - Click "Save [filename].gpx" button in the menu
   - File downloads with `_X` suffix to indicate it's been edited
   - Original file remains unchanged

### Advanced Features

#### Splitting Tracks

1. Click menu → Enable "Split Mode"
2. Tap on any point where you want to split
3. Review the split tracks in the menu
4. Save individual segments as needed
5. Exit split mode when done

#### Joining Tracks

1. Click menu → "Join Tracks" section
2. Click "Load Tracks to Join (multi-select)"
3. Select multiple GPX files (Ctrl+Click or Shift+Click)
4. Review the loaded tracks
5. Click "Join All Tracks"
6. Save the combined track

#### Auto-Simplification

Files with more than 5,000 points are automatically simplified when loaded:
- Uses the current slider setting (default 10%)
- Toast notification shows: `Auto-simplified at 10%: 790000 → 79000 points (Use 'Restore Original' to undo)`
- Always reversible with "Restore Original"

## File Format Support

- **Input**: `.gpx` files (GPX 1.0 and 1.1)
- **Output**: `.gpx` files with all original metadata preserved
- **Special handling**: Automatically cleans doubled dates from GeoTracker exports
  - Example: `2020-02-29_2020-02-29_Track.gpx` → `2020-02-29_Track.gpx`

## Performance

- **Small tracks** (<5,000 points): Instant processing
- **Medium tracks** (5,000-100,000 points): 1-3 seconds
- **Large tracks** (100,000-1,000,000 points): 5-15 seconds with auto-simplification
- Optimized for mobile devices

## Tips & Best Practices

### For Best Results

1. **Start with conservative simplification** (10-20%) and increase if needed
2. **Use Google Terrain** for hiking/outdoor tracks to see elevation contours
3. **Long-press carefully** - the 2.6s delay prevents accidental deletions
4. **Check "Restore Original"** is available before saving if you want to undo changes

### Common Workflows

**Cleaning up a recorded hike:**
1. Load track → Auto-simplifies to 10%
2. Check the result
3. If too aggressive, "Restore Original" and manually adjust slider to 5%
4. Save with `_X` suffix

**Extracting part of a long track:**
1. Load track
2. Enable Split Mode
3. Tap at start and end of desired section
4. Save the middle segment

**Combining daily segments into a trip:**
1. Record each day separately
2. Use "Load Tracks to Join (multi-select)"
3. Select all daily files
4. Join and save as complete trip

## Keyboard Shortcuts

- **Ctrl+A**: Select all (when editing code)
- **Escape**: Close menus/dialogs

## Browser Support

- Chrome/Edge (recommended)
- Safari (iOS/macOS)
- Firefox
- Any modern browser with JavaScript enabled

## Technical Details

- **Algorithm**: Douglas-Peucker line simplification
- **Mapping**: Leaflet.js 1.9.4
- **No server required**: Runs entirely in your browser
- **Privacy**: All processing happens locally - no data uploaded

## Changelog

### v4.9 (2026-02-09)
- Automatically removes doubled dates in filenames
- Cleaned filename also updated in GPX file header

### v4.8 (2026-02-09)
- Updated app descriptions to highlight Simplify feature
- Changed tagline to "Simplify, Edit, Split & Join GPS Tracks"

### v4.7 (2026-02-09)
- Enhanced auto-simplification message with 'Restore Original' reminder

### v4.6 (2026-02-09)
- Clarified multi-select capability for joining tracks

### v4.5 (2026-02-09)
- Removed redundant "Download GPX" button
- Fixed save button to display actual filename dynamically

### v4.4 (2026-02-09)
- Reverted to fast linear tolerance formula
- Optimized for large files (handles 790k+ points efficiently)

### v4.2 (2026-02-09)
- Reduced track line width by 30%
- Changed markers to transparent red circle outlines
- Added multiple map layer options

## License

MIT License - see [LICENSE](LICENSE) file for details

## Author

**Tony Gozdz** © 2026

## Contributing

This is a personal project, but suggestions and bug reports are welcome! Please open an issue on GitHub.

## Support

For issues or questions:
1. Check the **About** section in the app menu for usage tips
2. Open an issue on GitHub
3. Include your browser/device info and a description of the problem

---

**Made with ❤️ for outdoor enthusiasts and GPS data nerds**
