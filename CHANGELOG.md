# Changelog

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
