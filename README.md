# Dublin-Bus-Project-
# 🚌 Dublin Bus Reliability Analysis

A full data-engineering and machine-learning pipeline that collects live Dublin Bus GTFS-RT feeds, stores delay observations in a SQLite database, and produces reliability metrics, cluster profiles, and visualisations across the network.

> Completed as part of the **MSc in Artificial Intelligence** programme (H9DAI).

---

## Research Question

> Which Dublin Bus routes and regions are the least reliable, and do distinct reliability profiles exist across the network?

---

## Project Structure

```
PAI-Project/
├── pipeline/
│   ├── collect.py               # Live GTFS-RT ingestion
│   ├── data_collection.py
│   ├── data_cleaning.py
│   ├── database.py              # SQLite schema & connection helpers
│   ├── reliability_metrics.py   # Delay, on-time rate, cancellation rate
│   ├── clustering.py            # K-Means, Agglomerative, DBSCAN
│   ├── temporal_stability.py    # Day-of-week / hour-of-day profiles
│   ├── visualizations.py        # All figure generation
│   ├── route_region_lookup.py
│   ├── gtfs_static_loader.py
│   └── run_pipeline.py          # Entry point
├── results/                     # Generated figures (PNG + interactive HTML map)
├── presentation.ipynb
└── requirements.txt
```

---

## Methodology

**Data Collection**
- Polls the Dublin Bus GTFS-Realtime API at regular intervals
- Loads static GTFS (stops, routes, trips) into SQLite via `gtfs_static_loader.py`
- Cleans and validates observations, flags outliers and cancellations

**Reliability Metrics** (per route and per region)
- Mean delay, median delay, P85 / P95 delay
- On-time rate (|delay| ≤ 60 seconds)
- Cancellation rate

**Clustering**
- Features standardised with `StandardScaler`
- Three algorithms compared: K-Means, Agglomerative, DBSCAN
- Model selection via Silhouette Score, Davies-Bouldin Index, Calinski-Harabasz Score
- PCA scatter plots for each clustering result

**Temporal Stability**
- Day-of-week and hour-of-day reliability profiles per cluster
- Heatmaps of route stability across time windows

---

## Results

| Figure | Description |
|--------|-------------|
| `fig1` | Delay distributions by region |
| `fig2` | Cancellation rates by region |
| `fig3` | Route reliability heatmap |
| `fig4–6` | PCA scatter plots (K-Means, Agglomerative, DBSCAN) |
| `fig7` | K sweep metrics (elbow + silhouette) |
| `fig8` | Cluster reliability profiles |
| `fig9` | Interactive stop-reliability map (HTML) |
| `fig10` | Aggregation level comparison |
| `fig11` | Temporal cluster profiles |
| `fig12` | Route stability heatmap |
| `fig13` | Stability by cluster |
| `fig14` | Thursday vs Friday comparison |

---

## Setup & Installation

**Requirements:** Python 3.10+

```bash
pip install -r requirements.txt
```

**Run the full pipeline:**
```bash
python pipeline/run_pipeline.py
```

**Or open the presentation notebook:**
```bash
jupyter notebook presentation.ipynb
```

---

## Tech Stack

`Python` · `pandas` · `numpy` · `scikit-learn` · `matplotlib` · `seaborn` · `Folium` · `SQLAlchemy` · `SQLite` · `GTFS-realtime-bindings` · `protobuf` · `python-dotenv`

---

## License

Uses publicly available GTFS data from Dublin Bus / NTA. Used for academic research purposes only.

---

## Author

MSc Artificial Intelligence · H9DAI  
*Analytical design by the student; code built with AI-assisted development tools.*
