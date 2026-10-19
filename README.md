# SkinSurfaceRayTracing

## Code Availability

The source code for the ray-tracing simulations and subsequent analysis will be made publicly available upon publication of the associated scientific article.

## Data Availability

The generated skin surface geometries and simulated surface reflectance data used in this study are publicly available in this repository.

### Simulated Skin Surface Geometries

The 30 simulated skin surface geometries are stored in the `Data/` directory as compressed NumPy files (`.npz`), following the naming convention `lesion_{number}.npz`.

Each file contains the following arrays:

| Array | Shape | Description |
|-------|-------|-------------|
| `X` | (1000, 1000) | X-coordinates of the surface grid |
| `Y` | (1000, 1000) | Y-coordinates of the surface grid |
| `Z` | (1000, 1000) | Surface height values (Z-coordinates) |
| `N` | (1000, 1000) | Refractive index distribution |
| `N_all_wavelengths` | (1000, 1000, 1) | Refractive index distribution for the simulated wavelength (634 nm) |

#### Loading a Simulated Surface in Python

```python
import numpy as np

# Load the first simulated skin surface
data = np.load("Data/lesion_1.npz")

# Extract surface geometry and refractive index
X = data["X"]
Y = data["Y"]
Z = data["Z"]
N = data["N"]
N_all_wavelengths = data["N_all_wavelengths"]

# Display array shapes
for key in data.files:
    print(f"{key}: {data[key].shape}")
```

### Surface Reflectance Data

The simulated surface reflectance data are stored in `Thin_lens_model.npy` as a five-dimensional NumPy array with shape `(171, 171, 4, 1, 30)`.

The dimensions correspond to:

- **Axis 0 (171):** Detector x-coordinate (pixels).
- **Axis 1 (171):** Detector y-coordinate (pixels).
- **Axis 2 (4):** Illumination azimuthal angles (φ = 0°, 90°, 180°, 270°).
- **Axis 3 (1):** Wavelength (center wavelength: 634 nm).
- **Axis 4 (30):** Number of simulated skin surfaces.

**Array structure:** `reflectance[x, y, phi, wavelength, surface]`

Each simulated surface contains four spatially resolved reflectance images, corresponding to the four illumination angles at a center wavelength of 634 nm.

#### Loading the Data in Python

```python
import numpy as np

# Load simulated surface reflectance data
reflectance = np.load("Thin_lens_model.npy")

# Array shape: (x, y, phi, wavelength, surface)
print(reflectance.shape)  # (171, 171, 4, 1, 30)

# Extract reflectance image for the first surface
# at phi = 0° and wavelength = 634 nm
image = reflectance[:, :, 0, 0, 0]
```