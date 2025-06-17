# NDVI Time-Series Analysis and Visualization

This project performs time-series analysis of NDVI (Normalized Difference Vegetation Index) derived from Sentinel-2 satellite imagery. It includes NDVI calculation, spatial visualization, difference mapping, and video generation for vegetation monitoring across multiple years.

## Features

- Compute NDVI from NIR and Red bands of Sentinel-2 imagery
- Visualize NDVI maps per year with consistent color scaling
- Generate difference maps between years
- Plot mean NDVI over time
- Create NDVI animation (.mp4 or .gif) to visualize vegetation changes
- Modular structure for easy extension and automation

## NDVI Formula

The NDVI is computed as:

<div align="center"><strong>
NDVI = (NIR − Red) / (NIR + Red + ε)
</strong></div>

Where `ε` is a small number (e.g., 1e-6) to avoid division by zero.


Dependencies
Install required packages using:
``` python
pip install numpy matplotlib rasterio pillow
```
For .mp4 video generation, you also need:

FFmpeg (must be installed separately and available in your PATH)

Usage Overview
Prepare Data

Download Sentinel-2 bands (NIR and Red) as GeoTIFFs from Copernicus Browser

Store them in data/ folder with a dictionary mapping each year to band paths

Compute NDVI

``` python
def compute_ndvi(nir, red):
    nir = nir.astype('float32')
    red = red.astype('float32')
    return (nir - red) / (nir + red + 1e-6)
Visualize Yearly NDVI
```
``` python

def plot_ndvi(ndvi, title):
    ...
```

Plot NDVI Difference Between Years

``` python
diff = ndvi_data['2023']['ndvi'] - ndvi_data['2020']['ndvi']
Plot Mean NDVI Over Time
```
``` python
for year, data in ndvi_data.items():
    means.append(np.nanmean(data['ndvi']))
```
Create NDVI Time-Lapse

``` python
create_ndvi_video(ndvi_data, output_path='outputs/ndvi_video.mp4', fps=1)
```
Area of Interest (AOI)
To consistently download data for the same location, the project uses this bounding box:

```vbnet
Longitude:  7.543187 to 7.563872  
Latitude:  47.90029 to 47.913092
```
It is also available as a geojson file (aoi.geojson) for use in download portals or APIs.

License
This project is provided for educational and research purposes. No commercial use without permission.

Author: Bartosz Janikula
Contact: [your email or GitHub]
