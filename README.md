# 🔥 AGNI-DRISHTI
### AI-Assisted Forest Fire Early Warning & Response Intelligence

AGNI-DRISHTI is a geospatial intelligence platform designed to support forest-fire monitoring and response planning in Himachal Pradesh, India. It brings satellite-detected hotspots, available weather information, explainable risk assessment, and interactive mapping into one dashboard.

> **Important:** This is a decision-support prototype, not an official emergency-warning or dispatch system. Its outputs must not replace verified information or guidance from relevant authorities.

## 🌲 Project Overview

Forest fires can threaten ecosystems, wildlife, communities, and infrastructure. AGNI-DRISHTI aims to make relevant geospatial information easier to inspect by combining satellite observations, weather context, spatial analysis, and a map-driven interface.

## ✨ Key Features

- **🛰️ Satellite hotspot monitoring:** Integrates with NASA FIRMS when the service, network, and required credentials are available.
- **🗺️ Interactive map:** Explore observations, select markers, and inspect geographic context.
- **🌦️ Weather intelligence:** Retrieves available weather information and forecasts through Open-Meteo.
- **🤖 ML hotspot clustering:** Spatial clustering such as DBSCAN can group nearby detections. A cluster is not proof of one confirmed fire.
- **📊 Explainable risk assessment:** Shows a transparent heuristic assessment when its inputs are available; it is not automatically a trained predictive model.
- **🟥 Optional impacted-area layer:** A switchable overlay can display a verified perimeter, a defensible modeled scenario, or a clearly labeled illustrative demo polygon. It should be off by default.
- **🚨 Response intelligence:** Organizes observations and advisory information for human review.
- **🔎 Data transparency:** Live, demo, degraded, and unavailable states should be clearly distinguished.

## 🔄 How It Works

1. Retrieve satellite observations from NASA FIRMS when configured and available.
2. Validate and normalize coordinates, timestamps, and observation attributes.
3. Apply geographic filtering using reliable boundary data where available.
4. Retrieve weather context for supported coordinates.
5. Analyze observations with spatial clustering and documented risk logic where implemented.
6. Display results on the interactive dashboard.
7. Clearly identify stale, missing, synthetic, or unavailable data.

```text
NASA FIRMS ──► Validate observations ──► Geographic filtering ──┐
                                                               │
Open-Meteo ──► Weather context ─────────────────────────────────┤
                                                               ▼
                                               Clustering / risk assessment
                                                               │
                                                               ▼
                                                    FastAPI backend
                                                               │
                                                               ▼
                                                React map dashboard
```

## 🛠️ Technology Stack

| Area | Technology |
|---|---|
| Frontend | React, TypeScript, Vite |
| Styling | Tailwind CSS |
| Mapping | Leaflet, React Leaflet |
| Backend | Python, FastAPI, Pydantic, Uvicorn |
| Data processing | pandas, NumPy |
| Machine learning | scikit-learn |
| Satellite data | NASA FIRMS |
| Weather data | Open-Meteo |

Confirm the actual dependencies and commands against the current repository files.

## 🌐 Data Sources

- **NASA FIRMS:** https://firms.modaps.eosdis.nasa.gov/ — satellite-detected active-fire and thermal-anomaly observations. Access may require a MAP_KEY; latency and available fields vary by product.
- **Open-Meteo:** https://open-meteo.com/ — coordinate-based weather observations and forecasts.

A satellite hotspot is not, by itself, confirmation of a ground fire or an exact fire perimeter.

## 🧠 AI and Machine Learning

- **Spatial clustering:** DBSCAN can group nearby observations using an appropriate geographic distance calculation and documented parameters.
- **Explainable risk:** A documented rule-based score can provide a transparent baseline. Its inputs, missing data, and limitations should be visible.
- **Future fire-spread modeling:** Credible forecasts require suitable weather, terrain, vegetation/fuel data, a suitable model, and independent validation against observed fire progression. Hotspots and weather alone are insufficient to claim an accurate forecast.

Do not claim model accuracy or validated predictions without documented experiments on appropriate data.

## ⚠️ Data Integrity and Limitations

- Satellite detections can represent thermal anomalies and are not always confirmed ground fires.
- Cloud cover, sensor resolution, overpass timing, and delivery latency affect observations.
- Weather may be unavailable or may not represent exact conditions at an incident site.
- Geographic labels should come from reliable boundary or geocoding data, not guesses.
- Synthetic observations and illustrative polygons must be visibly labeled and kept separate from live data.
- A modeled or illustrative area is not a verified fire perimeter.
- Risk assessments are decision-support aids, not guarantees.

## 📁 Project Structure

Intended structure; actual filenames may differ:

```text
agni-drishti/
├── frontend/       # React + TypeScript dashboard
├── backend/        # FastAPI service
├── data/
│   ├── demo/       # Clearly labeled demo data
│   ├── raw/        # Optional source snapshots
│   ├── processed/  # Optional normalized data
│   └── schemas/    # Data contracts
├── scripts/        # Utility scripts
├── tests/          # Automated tests
└── docs/           # Architecture and technical notes
```

## 🚀 Getting Started

### Prerequisites

- Python version required by the backend configuration.
- Node.js and npm version required by `frontend/package.json`.
- A NASA FIRMS MAP_KEY for live FIRMS access.
- Internet access for upstream satellite and weather services.

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd agni-drishti
```

Replace the placeholder URL with your repository's URL.

### 2. Configure environment variables

Check the backend's `.env.example` or configuration code for the exact variable name used for your FIRMS key. Example only:

```env
FIRMS_MAP_KEY=your_firms_map_key_here
```

Never commit `.env` files or real API keys. The variable name above is illustrative; use the name expected by your implementation.

### 3. Install dependencies

Create and activate a Python virtual environment, then install from the dependency file that actually exists in the repository. For example:

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
source .venv/bin/activate
```

If `backend/requirements.txt` exists:

```bash
pip install -r backend/requirements.txt
```

Install frontend dependencies:

```bash
cd frontend
npm install
```

## ▶️ Running the Application

Run the backend and frontend in separate terminals using the commands defined by your project. A typical FastAPI command may look like:

```bash
uvicorn app.main:app --reload
```

Run it from the directory where the `app` package is importable; adjust the module path if needed.

Start the frontend:

```bash
cd frontend
npm run dev
```

Open the local URL printed by Vite. Prefer repository-specific run instructions if they exist.

## 🧪 Testing

Run the tests and checks configured in the repository. Common examples:

```bash
pytest
```

```bash
cd frontend
npm run build
```

Only describe tests as passing if they have actually been executed successfully.

## 🛣️ Future Improvements

- Improve live-data coverage and freshness monitoring.
- Validate geographic filtering against reliable Himachal Pradesh boundaries.
- Evaluate hotspot clustering with documented parameters.
- Obtain suitable historical data for model validation.
- Investigate defensible fire-spread simulation when required landscape inputs are available.
- Expand integration tests, caching, observability, and error handling.
- Improve accessibility and communication of uncertainty.

## 🤝 Contributing

Contributions are welcome. Please add tests for new behavior, document configuration changes, and keep live data separate from synthetic demo data. Avoid unsupported claims about accuracy or operational readiness.

## 📄 License

No license has been specified. Add a `LICENSE` file before distributing the project if you want to grant others explicit permissions to use, modify, or redistribute it.
