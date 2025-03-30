# smart_farming_advisor

AGRI_FARM Crop Monitoring Project
Overview
This project focuses on crop monitoring using remote sensing data, specifically Landsat 8 satellite imagery. The main purpose is to calculate and visualize the Normalized Difference Vegetation Index (NDVI), which is a key indicator of plant health and vegetation density.

##Features
Loading and processing Landsat 8 satellite imagery

Calculation of NDVI (Normalized Difference Vegetation Index)

Visualization of NDVI maps with appropriate color schemes

Handling of geospatial data using rasterio library

##Requirements
The project requires the following Python libraries:

numpy

rasterio

matplotlib

google.colab (for Google Colab integration)

You can install the required packages using pip:

text
pip install rasterio numpy matplotlib
Usage
Mount your Google Drive (if using Google Colab):

python
from google.colab import drive
drive.mount('/content/drive')
Load the Landsat 8 bands (red and near-infrared):

python
red_band_path = '/path/to/your/LC08_L2SP_142048_20240328_20240410_02_T1_SR_B3.TIF'
nir_band_path = '/path/to/your/LC08_L2SP_142048_20240328_20240410_02_T1_SR_B4.TIF'
Calculate NDVI:

python
import numpy as np
import rasterio
import matplotlib.pyplot as plt

with rasterio.open(red_band_path) as red_src, rasterio.open(nir_band_path) as nir_src:
    red_band = red_src.read(1).astype(float)
    nir_band = nir_src.read(1).astype(float)
    
    np.seterr(divide='ignore', invalid='ignore')
    ndvi = (nir_band - red_band) / (nir_band + red_band)
    ndvi[np.isnan(ndvi)] = 0
Visualize the NDVI:

python
plt.imshow(ndvi, cmap='RdYlGn')
plt.colorbar()
plt.title('NDVI')
plt.show()
Data
The project uses Landsat 8 Surface Reflectance data from March 28, 2024. Specifically:

Band 3 (Red): LC08_L2SP_142048_20240328_20240410_02_T1_SR_B3.TIF

Band 4 (Near Infrared): LC08_L2SP_142048_20240328_20240410_02_T1_SR_B4.TIF

NDVI Interpretation
The NDVI values range from -1 to 1:

Values close to 1 (green in visualization): Healthy vegetation

Values around 0 (yellow in visualization): Sparse vegetation or soil

Negative values (red in visualization): Water, snow, clouds, or non-vegetated surfaces

Future Enhancements
Potential future enhancements for this project could include:

Time series analysis of vegetation changes

Integration of other vegetation indices (EVI, SAVI, etc.)

Classification of land cover types

Crop health monitoring and yield prediction

License
This project is open-source and available for educational and research purposes.

Acknowledgements
USGS for providing Landsat 8 data

Rasterio and NumPy communities for their excellent libraries
