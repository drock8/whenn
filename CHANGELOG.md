# Changelog

## [2026-05-15] — Grid View

### Added
- **Grid view**: New card-based layout showing all cities at a glance — 2 columns on mobile, 2 on desktop
- **Home card**: Centered home timezone card at the top of the grid with large editable time
- **Tap-to-edit time on any card**: Tap a city's time, type a new time, and every other card (and the map) updates instantly to show that moment in each timezone
- **Two-way sync**: Time edits on the map update the grid and vice versa
- **Day/night card backgrounds**: Cards use the same warm amber (day) and deep dark (night) shading as the map overlay — no emoji icons
- **Date context on cards**: Shows date with "(tomorrow)" or "(yesterday)" only when a city is on a different day than the user
- **Drag to reorder**: Hold and drag cards to rearrange; custom order persists across sessions
- **Mobile tabs**: Map/Grid toggle at the bottom of the screen on mobile
- **Desktop side-by-side**: Map (55%) and grid (45%) shown together on desktop

### Changed
- **Controls bar**: Now floats over both views (fixed position) so search, Plan Ahead, and home picker work regardless of active view
- **Controls order**: Reordered to Search, Location, Plan Ahead — groups related controls together on mobile
- **Plan Ahead syncs to grid**: Setting a future time updates both map labels and grid cards

### Fixed
- **Home city selection**: Selecting Shanghai (or other cities sharing an IANA timezone with another city) no longer defaults to the first match — city name is now stored separately in localStorage

## [2026-05-14] — Progressive Web App

### Added
- **PWA support**: Whenn is now installable on iOS, Android, and desktop via "Add to Home Screen"
- **Offline support**: Service worker caches all assets for offline use
- **App manifest**: Standalone display mode, themed status bar, proper app naming
- **App icons**: Gradient "W" icon in SVG, PNG (192px, 512px), and Android maskable formats
- **Favicon**: SVG favicon with PNG fallback
- **iOS standalone mode**: `apple-mobile-web-app-capable` with `black-translucent` status bar

## [2026-04-16] — Mobile UX Improvements

### Fixed
- **City deletion on mobile**: Tapping the remove (✕) button now correctly deletes the city instead of the button disappearing without effect
- **Per-city "time there" input on mobile**: Fully separated touch and mouse event paths — on touch devices, `mouseenter`/`mouseleave` handlers are no longer attached, eliminating synthetic mouse event interference on iOS. Tap a city label to show the reverse time input; tap elsewhere to dismiss
- **Mobile city label interactions**: Tap shows the "time there" input field; long-press (hold) reveals the delete button — follows standard mobile UX patterns. Delete icon no longer appears on tap via CSS `:hover` bleed-through
- **Search input focus on iOS Safari**: The search field and other control panel inputs can now be focused and typed into on touch devices
- **Bottom controls centering on mobile**: Fixed controls bar being slightly off-center to the left in the mobile column layout
- **Plan Ahead panel width**: Helper text no longer expands the panel — now positioned absolutely below it to match the search field width
- **Date labels hidden behind controls on mobile**: Moved date indicator up on mobile so it sits above the controls stack

### Added
- **Open Graph image and meta tags**: Link sharing now shows a striking preview with "What time is it there?" tagline, city dots, and dark background
- Helper text under "Plan Ahead": "See what time it'll be everywhere" to clarify the feature's purpose

### Changed
- **App title**: 20% larger with a green-to-purple gradient
- **"Plan Ahead" label**: Now uses the same green-to-purple gradient
- **Plan Ahead helper text**: Moved inside the panel box instead of floating below it
- Map taps on mobile no longer attempt to add cities — use the search field instead, since the screen is too small for accurate tap targeting
- Touch panning and pinch-to-zoom continue to work as before

## [2026-04-16] — Initial Release
- Whenn — interactive world map timezone viewer
