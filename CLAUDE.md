# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What is Whenn

Whenn is a single-page interactive world timezone viewer. It renders a pannable/zoomable SVG world map with real-time city clocks, a day/night terminator overlay, and a "Plan Ahead" feature that shows what time a future moment will be across all pinned cities. Deployed at https://whenn.vercel.app.

## Project Structure

The entire app is a single `index.html` file (~1630 lines) with no build system, no dependencies, and no package manager. There is nothing to install, build, or compile — just open the file in a browser.

## Development

Open `index.html` directly in a browser, or serve it with any static file server:

```
python3 -m http.server 8000
```

There are no tests, no linter, and no CI pipeline.

## Architecture

Everything lives in `index.html`: CSS in a `<style>` block, HTML for the map and controls, and all JavaScript in a single `<script>` block. Key sections are delimited by `// ============` comment banners.

**Map rendering**: An SVG with 3 tiled copies of the world (left/center/right at x offsets -1000/0/1000) to enable infinite horizontal wrapping. Land geometry is a single path string (`WORLD_PATH`) from Natural Earth 110m. The viewBox is manipulated for pan/zoom.

**City database**: `CITIES_RAW` is a hardcoded array of ~290 cities as `[name, country, timezone, lat, lng]` tuples, converted to objects in `CITIES`. Adding a city means appending to this array.

**Coordinate system**: The SVG viewBox is 1000x500. `lngToSVGX`/`latToSVGY` convert geographic coordinates to SVG space. City labels are HTML elements absolutely positioned over the SVG using `svgToScreen` for coordinate conversion.

**Interaction model**: Mouse drag pans, wheel zooms, double-click zooms in. Touch devices use single-finger pan and pinch-to-zoom. On desktop, hovering a city label shows a reverse time input; on mobile, tap shows the input and long-press shows the delete button. Touch and mouse event paths are fully separated (no synthetic event interference on iOS).

**State persistence**: Selected cities and home timezone are stored in `localStorage` under keys `wtm3` and `wtm_home`. The `wtm3` key stores city name/country pairs as JSON.

**Solar terminator**: `updateDayNight` computes day/twilight/night overlay paths using solar declination and subsolar longitude. Updates every 60 seconds.

**Plan Ahead**: The `futureTime` input parses flexible time formats (e.g., "5pm", "17:00", "1430") via `parseTimeFlexible`, computes a UTC moment, then `tickLabels` shows what time that moment corresponds to in each city's timezone.
