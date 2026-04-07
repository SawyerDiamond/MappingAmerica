# Mapping America

An interactive kiosk-style map of the United States built with Vue 3, Mapbox GL, and Tauri. Visitors can explore community-submitted memories pinned to locations across the country — from the contiguous states to Alaska, Hawaii, and US territories.

## What it does

- **Globe map** with Mapbox GL, custom pin markers, and smooth fly-to navigation
- **Territory insets** in the sidebar for Alaska, Hawaii, Puerto Rico/USVI, Guam/Northern Marianas, and American Samoa
- **Location detail panel** — click any pin to see a photo, title, and description
- **Submit flow** — a QR code modal links visitors to the companion mobile app to add their own memory
- **Inactivity timer** — returns to the home screen after 5 minutes of no interaction
- **Live data** — locations fetched from the backend API on load with a manual refresh option

## Stack

- [Vue 3](https://vuejs.org/) + [Vite](https://vitejs.dev/)
- [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/)
- [Tailwind CSS v4](https://tailwindcss.com/)
- [Tauri v2](https://tauri.app/) for desktop packaging

## Development

```bash
npm install
npm run dev        # web dev server (localhost:1420)
npm run tauri dev  # full Tauri desktop app
npm run build      # production web build
npm run tauri build # packaged desktop app
```

## Environment

Create a `.env.local` file:

```
VITE_API_BASE=https://your-api-gateway-url
VITE_MAPBOX_TOKEN=pk.your_mapbox_token
```

## Backend

Locations are served by a separate AWS SAM backend (`MappingAmericaBackend`). Submissions come in through the companion mobile app (`MappingAmericaMobile`) and are reviewed before appearing on the map.
