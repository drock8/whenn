# PWA Conversion Plan for Whenn

## Context

Whenn is a static single-file web app with no build system. Converting to a PWA makes it installable on iOS/Android/desktop home screens and enables offline use — important for a timezone tool people reach for quickly. The app has zero external dependencies, so the caching story is simple.

## Files Created

### 1. `icons/icon.svg` — Master app icon
SVG icon with gradient "W" on dark background, matching the app's green-to-purple gradient (`#34d399` → `#8b5cf6`) and font family.

### 2. `icons/icon-maskable.svg` — Maskable variant
Same "W" but scaled down to fit within the 80% Android adaptive icon safe zone.

### 3. `icons/icon-192.png` and `icons/icon-512.png` — Rasterized icons
Generated from the SVG using Node.js canvas. Required by Chrome for the install prompt and splash screen.

### 4. `icons/icon-maskable-512.png` — Android adaptive icon
Generated from the maskable SVG so Android's icon masking doesn't clip the "W".

### 5. `manifest.json` — Web app manifest
- `name`: "Whenn — World Time Planner"
- `short_name`: "Whenn"
- `display`: "standalone" (hides browser chrome, keeps system status bar)
- `theme_color` / `background_color`: `#0a0e17` (matches app background)
- `orientation`: "any" (map works in both orientations)
- Icons: 192px PNG, 512px PNG, maskable 512px PNG, SVG

### 6. `sw.js` — Service worker
- **Strategy**: Cache-first (everything is static)
- **Pre-caches**: index.html, manifest.json, icons
- **Update mechanism**: Bump `CACHE_NAME` (e.g., `whenn-v1` → `whenn-v2`) on each deploy
- `skipWaiting()` + `clients.claim()` for immediate activation

## Files Modified

### 7. `index.html`

**Head section additions:**
- `<meta name="theme-color">` — colors Android status bar
- `<link rel="manifest">` — points to manifest.json
- `<link rel="icon">` — SVG favicon + PNG fallback
- `<link rel="apple-touch-icon">` — iOS home screen icon
- `<meta name="apple-mobile-web-app-capable">` — iOS standalone mode
- `<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">` — blends with dark theme
- `<meta name="apple-mobile-web-app-title">`

**Script section addition:**
- Service worker registration at end of script block

## Platform Notes

- **iOS**: Does not generate splash screens from manifest; uses `apple-touch-icon` for home screen icon; kills PWA background tabs aggressively (fine for Whenn — state persists in localStorage)
- **Android**: Requires 192px + 512px PNG icons and a fetch-handling service worker for install prompt
- **Vercel**: Serves static files from root by default; no vercel.json needed
- **Updates**: When deploying new versions, bump `CACHE_NAME` in `sw.js`

## Verification Checklist

1. Chrome DevTools → Application → Manifest: all fields parsed correctly
2. Application → Service Workers: SW registered and activated
3. Application → Cache Storage: assets cached
4. Network → Offline: app still loads
5. Lighthouse → PWA audit: passes installability
6. Android Chrome: "Add to Home Screen" prompt appears
7. iOS Safari: Share → Add to Home Screen launches in standalone mode
