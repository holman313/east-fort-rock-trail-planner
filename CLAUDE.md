# East Fort Rock OHV Trail Planner

Single-page trail route planner for the East Fort Rock OHV system in the Deschutes National Forest (central Oregon). Runs locally from `file://` — no server needed.

## Tech Stack
- Leaflet.js 1.9.4 for interactive map
- Vanilla HTML/CSS/JS, no build system
- 75 USFS trails (~340 miles) embedded inline as GeoJSON (~2MB)
- Data source: USDA Forest Service EDW_TrailNFSPublish_01 (April 2026)

## File Structure
Single file: `index.html` (~2.1MB total)
- Lines 1–170: HTML + CSS (dark sidebar, orange accent `#e06c00`)
- Lines 170–250: Sidebar HTML (filters, stats, route list)
- Lines 253–360: JS config, state, map init, base layers, legend
- Lines 360–560: JS functions (helpers, topology, rendering, filters, route mgmt, stats, GPX export)
- Lines 560+: `loadData()` with embedded GeoJSON, boot call

Original backup at `C:\Users\JeffHolman\Documents\east-fort-rock-trail-planner.html`

## Key Features
- 4 base layers: Carto, Esri Street/Topo/Satellite
- Trail segments color-coded by difficulty
- Click segments to build a route; sidebar shows segment list & total mileage
- Undo / Clear / GPX export
- Difficulty filter checkboxes
- 5 staging area markers: Camp II, China Hat, Road 25, Road 2510, South Lava
- Hover tooltips with trail name, distance, difficulty

## Difficulty System
Heuristic-based; right-click any segment to override (saved to localStorage):
- **Green `#2ecc71`** — Easiest: Learners Loops + backbone loops (10, 20, 30, 40, 50, 60, 90)
- **Blue `#3498db`** — More Difficult: everything else
- **Black `#222222`** — Most Difficult: MVUM_SYMBOL=12 + original short connectors <0.5mi
- **Red `#e74c3c`** — Shared Use Roads: 17 named USFS MVUM roads (data in shared-use-roads.geojson)

## Intersection Splitting
Trails split at intersections into ~2000 clickable segments from 98 original features. Uses snapped grid (0.00015°) for intersection detection.

## Labels
Each segment shows trail number (#20, #40) or road number (2510, 1849), colored to match difficulty. Segments <0.1mi (trails) or <0.15mi (roads) skip labels to reduce clutter.

## Auth
Password gate using SHA-256 hash. Password: `EFR#313!` (hash stored, not plaintext). Session persists in localStorage. Logout button (⊗) in sidebar header.

## Git / Deployment
- Remote: https://github.com/holman313/east-fort-rock-trail-planner
- Branch: master
- Ready for GitHub Pages: Settings → Pages → master branch → root /

## Planned Enhancements
- [ ] Deploy to GitHub Pages
- [ ] Search/filter trails by name or number
- [ ] GPS "Locate me" button
- [ ] Elevation profile for selected route
- [ ] Drag-to-reorder segments in sidebar
- [ ] Save/load named routes to localStorage
- [ ] Route summary (est. ride time, difficulty breakdown)
- [ ] Light/dark theme toggle
- [ ] Mobile-responsive layout (collapsible sidebar)
- [ ] Seasonal closure indicators (ATV_MANAGED date ranges in data)
- [ ] Clickable staging areas with driving directions link
- [ ] Firebase auth for multi-user
- [ ] Cloud-synced routes via Firestore
- [ ] Shareable route links
- [ ] Optimize file size (externalize GeoJSON, gzip)
