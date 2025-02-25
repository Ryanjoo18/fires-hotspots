# Fires and Hotspots

## Overview
This project analyzes fire hotspots in **South Sumatra** using **Sentinel-2** imagery and **FIRMS (Fire Information for Resource Management System)** data. The script visualizes fire-affected areas using different band combinations and overlays detected hotspots.

## Features
✅ Loads **Sentinel-2 Harmonized** surface reflectance dataset  
✅ Uses **FIRMS** data to detect and visualize fire hotspots  
✅ Applies **True Color (RGB), False Color (NIR/Red/Green), and SWIR/NIR/Red** visualizations  
✅ Computes and prints the **total number of hotspots** in the region  
✅ Displays an **interactive map** in Google Colab using `geemap`  
✅ Exports images to **Google Drive** for further analysis  

## Setup & Installation
### 1. Install Required Packages
Run the following command in **Google Colab** to install dependencies:
```python
!pip install -q earthengine-api geemap folium
```

### 2. Authenticate and Initialize Earth Engine
```python
import ee

ee.Authenticate()  # Run this once to authenticate

ee.Initialize()
```

## Running the Script
Copy and run the `Fires_and_Hotspots.ipynb` script (or the provided Colab cells). The script will:
1. Load **Sentinel-2** and **FIRMS** datasets.
2. Filter the images based on **date (Sep 29, 2023)** and **location (South Sumatra, Indonesia)**.
3. Generate **True Color, False Color (NIR), and SWIR composites**.
4. Overlay **fire hotspots** detected in the region.
5. Compute and print the **total number of detected hotspots**.
6. Display an **interactive map**.

## Exporting Processed Images to Google Drive
To export **True Color, False Color (843), and False Color SWIR (12/8/4)** images to **Google Drive**, use:
```python
def export_image(image, description):
    task = ee.batch.Export.image.toDrive(
        image=image,
        description=description,
        folder='earthengine',
        region=AOI,
        scale=100,
        maxPixels=1e9
    )
    task.start()
    print(f"Exporting {description} to Google Drive...")

export_image(S2_image.visualize(trueCol_vis), "True_Colour_Picture_432")
export_image(S2_image.visualize(falseCol_vis), "False_Colour_Picture_843")
export_image(S2_image.visualize(falseColSWIR_vis), "False_Colour_Picture_1284")
```

## Notes
- Ensure you have **Google Earth Engine API enabled**.
- Authentication (`ee.Authenticate()`) is required **only once** per session.
- If running in Colab, restart the runtime if you face any authentication errors.

## License
This project is released under the **MIT License**.
