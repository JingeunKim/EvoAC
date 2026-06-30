# EvoAC — Drone Search Path Planning Dataset

A dataset for UAV (drone) search path planning over a probability map of target locations.

---

## Overview

Given a heatmap representing the spatial distribution of a search target (particles), the goal is to plan an optimal UAV search path that maximizes coverage within the drone's operational constraints.

---

## Dataset Structure

```
dataset/
├── SRU.csv               # Drone specifications
├── 1h_20/                # 1-hour flight, 20×20 grid
│   ├── heatmap_values.csv
│   ├── heatmap_index.csv
│   └── heatmap_center_point.csv
├── 2h_20/                # 2-hour flight, 20×20 grid
│   └── ...
└── 3h_20/                # 3-hour flight, 20×20 grid
    └── ...
```

---

## File Descriptions

### 1. `heatmap_index.csv`
Defines the index of each cell in the 20×20 heatmap.

- Indices are expressed as `x/y`.
- `x` increases to the right (0 = leftmost), `y` increases upward (0 = bottom).
- Both `x` and `y` range from **0 to 19**.
- Use this file when expressing the search path as an ordered sequence of cell indices.

### 2. `heatmap_center_point.csv`
Provides the GPS coordinates of the center point of each heatmap cell.

- Delimiter: `,` (between cells); `/` (between longitude and latitude within a cell).
- Format: `longitude/latitude`
- Example: `133.45206871/38.294637095` → longitude `133.45206871`, latitude `38.294637095`
- Use this file when expressing path vertices as geographic coordinates.

### 3. `heatmap_values.csv`
Contains the value of each heatmap cell — the number of particles (search targets) within that cell.

- The heatmap is **20×20** in size.
- Each cell covers approximately **1.03 km (width) × 0.5 km (height)**.
- Delimiter: `,`
- Example: cell (0, 0) has a value of `1`.

### 4. `SRU.csv`
Specifies the search drone's operational parameters.

- The total path length must satisfy:  
  **path length ≤ available search time × drone speed**
- Delimiter: `,`

---

## Notes

- All CSV files use `,` as the delimiter.
- The heatmap size is fixed at **20×20 cells**.
- Folder names follow the convention `{flight_hours}h_{grid_size}` (e.g., `2h_20` = 2-hour flight with a 20×20 heatmap grid).
