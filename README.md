# SKIP-PV Multimodal Dataset

This repository provides the processed **SKIP-PV multimodal dataset** used for photovoltaic (PV) forecasting research.  
The dataset integrates three modalities at each timestamp:

- **Sky images**
- **PV power output**
- **Meteorological and radiation variables**

The data are organized into a single HDF5 file with predefined **training/validation** and **test** splits, together with separate timestamp files stored in NumPy format.

---

## Download

The dataset is publicly available on Zenodo:

**DOI:** `10.5281/zenodo.18920659`

---

## Dataset Files

The release contains the following files:

- `data.h5`  
  Main HDF5 file containing all samples and variables
- `times_trainval.npy`  
  Timestamp array for the `/trainval` split
- `times_test.npy`  
  Timestamp array for the `/test` split
- `data_dictionary.csv`  
  Variable dictionary and safe-name mapping for programmatic use

---

## Dataset Organization

The HDF5 file contains two groups:

- `/trainval` — training/validation split
- `/test` — held-out test split

Each group contains the same set of variables.  
Each row corresponds to **one timestamped sample**.

### Split sizes

- `/trainval`: **349,372** samples
- `/test`: **14,003** samples

### Timestamp files

Timestamps are stored separately from the HDF5 file:

- `times_trainval.npy` → length = **349,372**
- `times_test.npy` → length = **14,003**

The order of timestamps exactly matches the sample order in the corresponding HDF5 group.

---

## Modalities and Variables

### 1. Sky image
- **Dataset name:** `images_log`
- **Shape:** `(N, 64, 64, 3)`
- **Data type:** `uint8`

This variable stores the sky images associated with each timestamp.

### 2. PV output (prediction target)
- **Dataset name:** `pv_log`
- **Shape:** `(N,)`
- **Data type:** `float64`

This variable represents the PV power output corresponding to each timestamp.

### 3. Meteorological and radiation features
In addition to images and PV output, each sample includes **18 scalar meteorological/radiation variables**, each stored as a one-dimensional dataset of shape `(N,)`.

These variables may include units and special characters in their original HDF5 dataset names (for example, `°C` or `W_m²`).

---

## Variable Naming

To preserve semantic clarity, the original dataset names inside the HDF5 file retain their physical units and special characters.  
However, these names may be inconvenient for coding or cross-platform processing.

For easier use in Python and other scripts, a safe-name mapping is provided in:

- `data_dictionary.csv`

This file maps:
- original HDF5 dataset names
- human-readable descriptions
- code-safe variable names

Users are encouraged to use the safe names in downstream preprocessing and model development.

---

## Example HDF5 Structure

```text
data.h5
├── /trainval
│   ├── images_log
│   ├── pv_log
│   ├── <18 meteorological/radiation variables>
│
└── /test
    ├── images_log
    ├── pv_log
    ├── <18 meteorological/radiation variables>
