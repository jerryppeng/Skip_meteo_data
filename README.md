# Dataset Overview (SKIP PV multi-modal dataset)

This dataset is stored in a single HDF5 file with two groups:
- `/trainval`: training/validation split
- `/test`: test split

Each group contains the same 20 datasets (variables). One row corresponds to one timestamp.
Timestamps are stored separately in NumPy files (e.g., `times_trainval.npy`, `times_test.npy`).

## File structure
- `data.h5` (HDF5)
  - `/trainval` (349,372 samples)
  - `/test` (14,003 samples)
- `times_trainval.npy` (length = 349,372)
- `times_test.npy` (length = 14,003)

## Modalities
- **Sky image**: `images_log` with shape `(N, 64, 64, 3)` and dtype `uint8`
- **PV output (target)**: `pv_log` with shape `(N,)` and dtype `float64`
- **Meteorological & radiation features**: 18 variables with shape `(N,)`

## Notes
- Dataset names inside HDF5 include units and special characters (e.g., `°C`, `W_m²`).
  For easier use in code, a safe-name mapping is provided in `data_dictionary.csv`.
