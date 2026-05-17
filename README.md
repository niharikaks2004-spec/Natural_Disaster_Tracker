# 🌍 Agnirva Natural Disaster Tracker

A real-time, interactive global disaster map that aggregates live data from three major scientific APIs — visualizing earthquakes, wildfires, floods, volcanoes, and landslides on a beautiful, fully-featured web interface. No backend. No dependencies to install. Open the file and go.

---

## ✨ Features

### 🗺️ Interactive World Map
- Powered by **Leaflet.js** with four switchable tile layers: Dark, Light, Satellite, and Terrain
- Smooth zoom, pan, and auto-fit controls
- Click any marker to see a popup with event name, date, source, magnitude (for earthquakes), and severity badge

### ⚡ Live Multi-Source Data Fetching
Pulls from three free, public APIs simultaneously:

| Source | Data |
|--------|------|
| **USGS Earthquake Hazards** | Earthquakes M ≥ 4.5 worldwide |
| **NASA EONET** | Wildfires, volcanoes, floods, landslides |
| **ReliefWeb** | Humanitarian flood and landslide reports |

- Configurable lookback window (default: 30 days, supports multi-year ranges)
- Chunked, paginated fetching with real-time progress bar and status messages
- Deduplication across sources to avoid duplicate events

### 🎨 Customizable Appearance
- **Light / Dark mode** toggle
- **Four marker styles:**
  - ⬤ Colored Circles (default)
  - 🔴 Severity-Scaled (size reflects high / medium / low)
  - 💫 Pulsing Rings (animated)
  - 🔥 Heat Dots (radial gradient blobs)
- Floating appearance panel accessible from the toolbar

### 📊 Analytics Sidebar
Live statistics panel that updates with every filter change:
- Total event count and active date window
- Breakdown by disaster category with animated bar charts
- Severity distribution (High / Medium / Low)
- Events-over-time timeline histogram
- Source attribution breakdown

### 🔍 Filtering & Search
- Filter by disaster category (Flood, Earthquake, Wildfire, Volcano, Landslide)
- Full-text search across event titles
- Fit-map button to auto-zoom to filtered results

### 📥 CSV Export
Export the current filtered view to a CSV file with columns: Type, Title, Date, Latitude, Longitude, Magnitude, Source, Severity.

---

## 🚀 Getting Started

No installation required. This is a single self-contained HTML file.

1. **Download** `AgnirvaNaturalDisasterTracker.html`
2. **Open** it in any modern browser (Chrome, Firefox, Edge, Safari)
3. Click **⚡ Fetch Data** to load live events
4. Explore the map, adjust filters, and toggle the stats sidebar

> An internet connection is required to fetch live disaster data and load map tiles.

---

## 🛠️ Usage

### Fetching Data
- Set the **Days back** field to control how far back to fetch (e.g. `7` for the past week, `365` for a year)
- Click **⚡ Fetch Data** — a progress overlay will show the status of each API call in real time
- The header badge updates with the last fetch timestamp once complete

### Filtering Events
- Use the **Category** dropdown to isolate a single disaster type
- Use the **Search** box to filter by location name or event title
- Click **⊞ Fit Map** to auto-zoom the map to all visible markers

### Customizing the Map
- Click the **🎨** button in the top-right to open the appearance panel
- Switch between Dark, Light, Satellite, and Terrain base maps
- Change the marker style — pulsing rings work great for recent events; heat dots give a density feel

### Exporting Data
- Apply any filters you want, then click **↓ Export CSV**
- A file named `agnirva_YYYY-MM-DD.csv` will download automatically

---

## 🧱 Tech Stack

| Technology | Purpose |
|------------|---------|
| **HTML / CSS / JavaScript** | Single-file app, no build step |
| **Leaflet.js v1.9.4** | Interactive map rendering |
| **USGS FDSN Web Services** | Earthquake data |
| **NASA EONET API v3** | Natural event tracking |
| **ReliefWeb API v1** | Humanitarian disaster reports |
| **Google Fonts** | Inter + Space Mono typefaces |
| **CARTO / OSM / Esri / OpenTopoMap** | Map tile providers |

---

## 📡 Data Sources

### USGS Earthquake Hazards Program
- Endpoint: `https://earthquake.usgs.gov/fdsnws/event/1/query`
- Fetches M ≥ 4.5 earthquakes (threshold scales up automatically for longer date ranges)
- Paginated in chunks of 2,000 events per request

### NASA Earth Observatory Natural Event Tracker (EONET)
- Endpoint: `https://eonet.gsfc.nasa.gov/api/v3/events`
- Categories: `wildfires`, `volcanoes`, `floods`, `landslides`
- Up to 2,500 events per category per date chunk

### ReliefWeb
- Endpoint: `https://api.reliefweb.int/v1/disasters`
- Covers floods and landslides with humanitarian context and country-level geolocation
- Paginated POST requests, up to 1,000 records per disaster type

---

## ⚙️ Configuration

All configuration is done directly in the UI. For deeper customization, the top of the script section contains easy-to-edit constants:

```javascript
const COLORS = {
  FLOOD: '#3b9de8',
  LANDSLIDE: '#c8a06a',
  VOLCANO: '#e85d3b',
  WILDFIRE: '#f0a04b',
  EARTHQUAKE: '#c084fc'
};
```

Severity thresholds for earthquakes:

| Magnitude | Severity |
|-----------|----------|
| ≥ 7.0 | 🔴 High |
| ≥ 5.5 | 🟠 Medium |
| < 5.5 | 🟢 Low |

---

## 📁 Project Structure

This is a single-file project — everything lives in one `.html` file:

```
AgnirvaNaturalDisasterTracker.html
├── <head>          — External CDN links (Leaflet, Google Fonts)
├── <style>         — All CSS (CSS variables, dark/light themes, layout)
├── <body>          — HTML structure (header, controls, map, sidebar, overlays)
└── <script>        — All JavaScript (map init, API fetching, rendering, UI logic)
```

---

## 🌐 Browser Compatibility

| Browser | Supported |
|---------|-----------|
| Chrome 90+ | ✅ |
| Firefox 88+ | ✅ |
| Edge 90+ | ✅ |
| Safari 14+ | ✅ |

---

## 🤝 Contributing

Contributions are welcome! Some ideas for future improvements:

- Add more disaster categories (hurricanes, tsunamis, drought)
- Clustering for high-density regions
- Time-scrubber to animate events over time
- Offline mode with cached data
- Additional data sources (GDACS, PDC)

Feel free to open an issue or submit a pull request.

---

## 📄 License

This project is open source. Data is sourced from public APIs provided by USGS, NASA, and ReliefWeb — please review their respective terms of use before deploying at scale.

---

## 🙏 Acknowledgements

- [USGS Earthquake Hazards Program](https://earthquake.usgs.gov/) for real-time seismic data
- [NASA EONET](https://eonet.gsfc.nasa.gov/) for satellite-tracked natural events
- [ReliefWeb](https://reliefweb.int/) for humanitarian disaster reporting
- [Leaflet.js](https://leafletjs.com/) for the excellent open-source mapping library
- [CARTO](https://carto.com/), [OpenStreetMap](https://www.openstreetmap.org/), [Esri](https://www.esri.com/), and [OpenTopoMap](https://opentopomap.org/) for map tiles

---

<p align="center">Built with ❤️ by Agnirva</p>
