# GeoRisk AI

Flood and land-change mapping from Sentinel-1/2 satellite imagery, with an API and dashboard for flagging at-risk infrastructure.

Problem

Floods damage roads, bridges, buildings and farmland every monsoon season. Optical satellite imagery is often blocked by cloud cover during floods, and manual mapping is slow. Civil and planning teams need fast, repeatable estimates of flood extent and the infrastructure it affects.

What this project does
Downloads Sentinel-1 (SAR) and Sentinel-2 (optical) imagery for a chosen river basin.
Preprocesses it: cloud masking, spectral indices (NDWI, MNDWI, NDVI), tiling.
Segments water/flood pixels with a Random Forest baseline and a U-Net (PyTorch).
Compares pre- and post-monsoon imagery to estimate flooded area.
Overlays OpenStreetMap roads and buildings to flag at-risk infrastructure.
Serves predictions through a FastAPI service and a web dashboard.

Tech stack
Language: Python
Geospatial: rasterio, geopandas, shapely, xarray, OSMnx
ML: scikit-learn, PyTorch
Backend: FastAPI, PostgreSQL + PostGIS
Frontend: Streamlit (or Leaflet)
DevOps: Docker, GitHub Actions, AWS (or GCP/Azure)
Quality: pytest, ruff, bandi

AI-assisted development

AI coding assistants were used for boilerplate, test scaffolding and documentation drafts. All generated code was reviewed, tested and modified before being committed.
