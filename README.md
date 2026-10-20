# GeoRisk AI

Flood and land-change mapping from Sentinel-1/2 satellite imagery, with an API and dashboard for flagging at-risk infrastructure.

## Problem

Floods damage roads, bridges, buildings and farmland every monsoon season. Optical satellite imagery is often blocked by cloud cover during floods, and manual mapping is slow. Civil and planning teams need fast, repeatable estimates of flood extent and the infrastructure it affects.

## What this project does

1. Downloads Sentinel-1 (SAR) and Sentinel-2 (optical) imagery for a chosen river basin.
2. Preprocesses it: cloud masking, spectral indices (NDWI, MNDWI, NDVI), tiling.
3. Segments water/flood pixels with a Random Forest baseline and a U-Net (PyTorch).
4. Compares pre- and post-monsoon imagery to estimate flooded area.
5. Overlays OpenStreetMap roads and buildings to flag at-risk infrastructure.
6. Serves predictions through a FastAPI service and a web dashboard.

## Architecture

```
Sentinel-1/2 data
      |
      v
Preprocessing (rasterio, geopandas, xarray)
      |
      v
Model training / inference (scikit-learn, PyTorch)
      |
      v
FastAPI service  <-->  PostgreSQL + PostGIS
      |
      v
Dashboard (Streamlit / Leaflet)
```

## Tech stack

- **Language:** Python
- **Geospatial:** rasterio, geopandas, shapely, xarray, OSMnx
- **ML:** scikit-learn, PyTorch
- **Backend:** FastAPI, PostgreSQL + PostGIS
- **Frontend:** Streamlit (or Leaflet)
- **DevOps:** Docker, GitHub Actions, AWS (or GCP/Azure)
- **Quality:** pytest, ruff, bandit

## Project structure

```
georisk-ai/
├── src/georisk/
│   ├── data/          # download and loading
│   ├── preprocess/    # cloud masks, indices, tiling
│   ├── models/        # baseline and U-Net
│   └── api/           # FastAPI app
├── tests/
├── notebooks/         # exploratory analysis only
├── docs/
└── .github/workflows/ci.yml
```

## Getting started

```bash
git clone https://github.com/<your-username>/georisk-ai.git
cd georisk-ai
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env             # add your own credentials
pytest
```

Run the API locally:

```bash
uvicorn georisk.api.main:app --reload
```

## Data

- Sentinel-1/2 imagery from the Copernicus Data Space or Google Earth Engine
- Labeled flood data for training: Sen1Floods11
- Roads and buildings: OpenStreetMap

Raw data is not stored in this repo. Use the download scripts in `src/georisk/data/`.

## Results

_To be filled in after training. Only real numbers go here._

| Model | IoU | F1 | Notes |
|---|---|---|---|
| Random Forest (baseline) | TBD | TBD | |
| U-Net | TBD | TBD | |

Include:
- Sample prediction vs. ground truth
- Performance on a region the model never saw during training

## Validation and limitations

Model output is checked, not trusted. Planned checks:

- Hold-out evaluation on an unseen region and season
- Error analysis on known failure cases: shadows, turbid water, cloud residue, urban areas
- Manual spot-checks against high-resolution imagery

Known limitations will be documented here as they are found.

## Quality and engineering practices

- Unit tests for preprocessing and API endpoints (`pytest`)
- Linting and formatting with `ruff`
- Security scanning with `bandit`
- CI on every push and pull request via GitHub Actions
- Feature branches and pull-request reviews
- Core logic packaged as a reusable library (`georisk`)

## Roadmap

-  Repository skeleton and CI
-  Data download and loading
-  Spectral indices (NDWI, MNDWI, NDVI) with tests
-  Random Forest baseline
-  U-Net training and evaluation
-  Change detection (pre vs. post flood)
-  OSM overlay for at-risk infrastructure
-  FastAPI service
-  Dashboard
-  Dockerize and deploy
-  Demo video and model card

## AI-assisted development

AI coding assistants were used for boilerplate, test scaffolding and documentation drafts. All generated code was reviewed, tested and modified before being committed.
