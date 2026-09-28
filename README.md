# Compound Low-Flow Heat Wave Analysis

Code and figure-reproduction notebooks accompanying an analysis of compound
low-flow / heat-wave events (CE) over Europe, built on HERA discharge
reanalysis, E-OBS v31.0e / ECA&D temperature data, and EARLS basin
shapefiles. The detection method itself is dataset-agnostic: it can be
scaled to any runoff dataset (e.g. HERA or EARLS) combined with any
temperature dataset.

This code is part of the article "Rising frequency and spatial extent of
concurrent low-flow–heatwave events across European rivers since 1960"

## Repository contents

- `CE_Detection_Analysis_HERA.ipynb` — a worked example of the low-flow /
  heat-wave compound-event detection method for a single grid cell, using
  HERA discharge and E-OBS v31.0e temperature data (via ECA&D thresholds).
  The method is not specific to this grid cell or these datasets: it
  generalizes to any runoff dataset (e.g. HERA, EARLS) paired with any
  temperature dataset, by pointing the notebook's inputs at the desired
  discharge and temperature time series.
- `MainFigureScript.ipynb` — reproduces the main text figures from
  pre-computed data in `FigData/`.
- `SuppFigureScript.ipynb` — reproduces the supplementary figures from
  pre-computed data in `FigData/`.
- `Data/` — single-gridcell input time series used by
  `CE_Detection_Analysis_HERA.ipynb`.
- `FigData/` — pre-computed/aggregated data (NetCDF, parquet, CSV, JSON,
  shapefiles) used to draw the figures directly, without rerunning the full
  processing pipeline.
- `Figure/` — output directory the notebooks save rendered figures into.

Everything needed to *reproduce the published figures* from the provided `FigData/`, is self contained in the three notebooks above.

## Setup

The geospatial stack used here (`cartopy`, `geopandas`) depends on system
libraries (GDAL, GEOS, PROJ) that are not always reliable to install with
plain `pip` on every platform. **Conda/mamba is recommended**:

```bash
conda create -n compound-events python=3.10
conda activate compound-events
conda install -c conda-forge --file requirements.txt
```

Alternatively, with `pip` (works well on Linux/macOS if GDAL/GEOS/PROJ are
already available, e.g. via Homebrew: `brew install gdal geos proj`):

```bash
python -m venv .venv
source .venv/bin/activate   # .venv\Scripts\activate on Windows
pip install -r requirements.txt
```

Then launch Jupyter:

```bash
jupyter notebook
```

## Running the notebooks

Each notebook resolves its own `Data/` / `FigData/` / `Figure/` paths
relative to its own location, so no manual path configuration is needed —
just run the notebooks from a checkout of this repository with the folder
structure intact, in any order:

1. `CE_Detection_Analysis_HERA.ipynb`
2. `MainFigureScript.ipynb`
3. `SuppFigureScript.ipynb`

## Data availability

If large data files in `Data/` or `FigData/` are not included in this
repository (see repository size notes), they are available at: **[add your
data hosting link here, e.g. Zenodo/OSF DOI]**.

## License

Code in this repository is released under the [MIT License](LICENSE).
