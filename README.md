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
VITE_API_BASE_URL=https://your-api-gateway-url
VITE_MAPBOX_TOKEN=pk.your_mapbox_token
```

## Building for Raspberry Pi

The simplest approach is to build directly on the Pi rather than cross-compiling.

**1. Install system dependencies**

```bash
sudo apt update && sudo apt install -y \
  libwebkit2gtk-4.1-dev libgtk-3-dev \
  libayatana-appindicator3-dev librsvg2-dev \
  curl build-essential
```

**2. Install Rust**

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
```

**3. Install Node.js**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install 20
```

**4. Clone and build**

```bash
git clone https://github.com/SawyerDiamond/MappingAmerica
cd MappingAmerica
npm install
npm run tauri build
```

The installer lands at `src-tauri/target/release/bundle/deb/*.deb`. Install it with:

```bash
sudo dpkg -i src-tauri/target/release/bundle/deb/*.deb
```

**Kiosk autostart**

To launch automatically on boot, create an autostart entry:

```bash
mkdir -p ~/.config/autostart
cat > ~/.config/autostart/mapping-america.desktop << EOF
[Desktop Entry]
Type=Application
Name=Mapping America
Exec=/usr/bin/mapping-america
X-GNOME-Autostart-enabled=true
EOF
```

Requires a desktop environment running (LXDE, GNOME, etc.) — not a headless/CLI boot.

## Backend

Locations are served by a separate AWS SAM backend (`MappingAmericaBackend`). Submissions come in through the companion mobile app (`MappingAmericaMobile`) and are reviewed before appearing on the map.
