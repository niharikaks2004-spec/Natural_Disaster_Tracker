# Agnirva Natural Disaster Tracker 🌍

A powerful, real-time global disaster monitoring web application that aggregates live data from three major scientific APIs and plots it on a fully interactive world map.
Track earthquakes, wildfires, floods, volcanoes, and landslides — filtered, searchable, and exportable — all from a single self-contained HTML file with zero installation required.

![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23F7DF1E.svg?style=for-the-badge&logo=javascript&logoColor=black)
![Leaflet](https://img.shields.io/badge/Leaflet-v1.9.4-199900?style=for-the-badge&logo=leaflet&logoColor=white)
![NASA EONET](https://img.shields.io/badge/NASA_EONET-API_v3-0B3D91?style=for-the-badge&logoColor=white)
![USGS](https://img.shields.io/badge/USGS-Earthquake_API-green?style=for-the-badge&logoColor=white)

---

## 🛠 Features

### 1. Interactive World Map
* **Four Switchable Tile Layers:** Toggle between 🌑 Dark (CARTO), ☀️ Light (OpenStreetMap), 🛰 Satellite (Esri), and 🏔 Terrain (OpenTopoMap) base maps on the fly.
* **Clickable Event Markers:** Every plotted event opens a popup with its name, date, data source, magnitude (for earthquakes), and a colour-coded severity badge.
* **Auto-Fit Viewport:** The **⊞ Fit Map** button auto-zooms and pans the map to frame all currently visible markers perfectly.

### 2. Live Multi-Source Data Fetching
* **Three Public APIs in Parallel:** Pulls simultaneously from USGS (earthquakes), NASA EONET (wildfires, volcanoes, floods, landslides), and ReliefWeb (humanitarian flood and landslide reports).
* **Configurable Lookback Window:** Set any number of days — from 1 to several years — to control the date range of fetched events.
* **Chunked Paginated Requests:** Long date ranges are automatically split into smaller chunks per API to respect endpoint limits, with a real-time progress bar and per-chunk status messages shown during loading.
* **Cross-Source Deduplication:** Events already present from one source are not re-added when encountered in another.

### 3. Customizable Marker Appearance
* **Four Distinct Marker Styles:**
  * ⬤ `Colored Circles` — Clean category-coloured rings (default)
  * 🔴 `Severity Scaled` — Circle size reflects event severity (High / Medium / Low)
  * 💫 `Pulsing Rings` — Animated expanding ring effect for a live-radar feel
  * 🔥 `Heat Dots` — Radial gradient blobs that evoke a heat-density aesthetic
* **Light / Dark Mode Toggle:** Full UI theme switch, with the map tile automatically following the selected mode.
* **Floating Appearance Panel:** Accessible via the 🎨 toolbar button; closes on outside click without disrupting the map.

### 4. Analytics Sidebar
* **Live Statistics Panel:** Updates in real time whenever filters change, showing total event count and active date window.
* **Category Breakdown:** Animated bar chart comparing event counts across all five disaster types.
* **Severity Distribution:** High / Medium / Low grid with counts (earthquake severity derived from magnitude; all other types default to Medium).
* **Events-Over-Time Histogram:** A bucketed timeline bar chart spanning the fetched date range.
* **Source Attribution Table:** Per-source event counts so you can see exactly where the data came from.

### 5. Filtering, Search & Export
* **Category Filter:** Instantly isolate any single disaster type from the dropdown.
* **Live Text Search:** Filter markers and sidebar stats in real time by typing any keyword from an event's title or location name.
* **CSV Export:** Downloads the current filtered dataset as `agnirva_YYYY-MM-DD.csv` with columns for Type, Title, Date, Latitude, Longitude, Magnitude, Source, and Severity.

---

## 📂 File Architecture & Technology Stack

The complete application is a self-contained **Single Page Application (SPA)** — one `.html` file, no build step, no package manager, no server needed:

* **Frontend Structure:** Semantic HTML5 layout split into header, controls bar, info bar, map viewport, floating appearance panel, collapsible analytics sidebar, loading overlay, and toast notification layer.
* **Style Engine:** Vanilla CSS3 built on a full set of custom atomic variables (`--bg`, `--surface`, `--accent`, `--flood`, `--earthquake`, etc.), smooth `@keyframes` animations (`pulseRing`, `spin`, `fadeIn`), and a fluid layout constructed with Flexbox.
* **Logic Controller:** Native JavaScript (ES6+) managing asynchronous multi-source API fetching, chunked pagination, Leaflet marker lifecycle, real-time DOM filtering, sidebar chart rendering, light/dark theming, and CSV export — all without any framework.

---

## 🚀 Getting Started

### Prerequisites
* A modern web browser (Chrome, Firefox, Edge, or Safari).
* An active internet connection (required to fetch live data and load map tiles).
* No API keys needed — all three data sources are fully public and free.

### Installation & Launch
1. Clone this repository or download the `.html` file directly:
   ```bash
   git clone https://github.com/niharikaks2004-spec/agnirva-disaster-tracker.git
   ```
2. Open the file in your browser:
   ```bash
   open AgnirvaNaturalDisasterTracker.html
   # or just double-click the file
   ```
3. Click **⚡ Fetch Data** in the toolbar to load live events onto the map.

---

## 📡 Data Sources

| Source | Disaster Types | API Endpoint |
| :--- | :--- | :--- |
| **USGS Earthquake Hazards Program** | Earthquakes (M ≥ 4.5) | `earthquake.usgs.gov/fdsnws/event/1/query` |
| **NASA Earth Observatory Natural Event Tracker (EONET) v3** | Wildfires, Volcanoes, Floods, Landslides | `eonet.gsfc.nasa.gov/api/v3/events` |
| **ReliefWeb API v1** | Floods, Landslides (humanitarian reports) | `api.reliefweb.int/v1/disasters` |

Magnitude thresholds for USGS queries scale automatically with the requested date range — longer windows use a higher minimum magnitude to keep response sizes manageable.

---

## ⚙️ Severity Classification

Severity is computed per event and drives both the sidebar statistics and the **Severity Scaled** marker style:

| Condition | Severity |
| :--- | :--- |
| Earthquake M ≥ 7.0 | 🔴 High |
| Earthquake M ≥ 5.5 | 🟠 Medium |
| Earthquake M < 5.5 | 🟢 Low |
| All other disaster types | 🟠 Medium (default) |

---

## 🌐 Browser Compatibility

| Browser | Supported |
| :--- | :--- |
| Chrome 90+ | ✅ |
| Firefox 88+ | ✅ |
| Edge 90+ | ✅ |
| Safari 14+ | ✅ |

---

## 🤝 Contributing

Contributions are welcome! Some ideas for future enhancements:

* Add hurricane, tsunami, and drought categories
* Marker clustering for high-density regions
* A time-scrubber to animate events chronologically across the map
* GDACS or PDC as additional data sources
* Offline mode with locally cached data

Feel free to open an issue or submit a pull request.

---

## 📄 License

This project is open source. Data is provided by USGS, NASA, and ReliefWeb under their respective public-use terms — please review those terms before deploying at scale or building a commercial product on top of this.

---

## 🙏 Acknowledgements

* [USGS Earthquake Hazards Program](https://earthquake.usgs.gov/) for real-time global seismic data
* [NASA EONET](https://eonet.gsfc.nasa.gov/) for satellite-tracked natural event feeds
* [ReliefWeb](https://reliefweb.int/) for humanitarian disaster reporting
* [Leaflet.js](https://leafletjs.com/) for the open-source interactive mapping library
* [CARTO](https://carto.com/), [OpenStreetMap](https://www.openstreetmap.org/), [Esri](https://www.esri.com/), and [OpenTopoMap](https://opentopomap.org/) for map tile layers

---

<p align="center">Built with ❤️ by Agnirva</p>
