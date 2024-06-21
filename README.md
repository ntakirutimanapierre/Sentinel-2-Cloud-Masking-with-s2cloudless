# Sentinel-2 Cloud Masking with s2cloudless

## Overview

This document provides a detailed walkthrough of the process of masking clouds and cloud shadows in Sentinel-2 (S2) surface reflectance (SR) data using the `s2cloudless` algorithm with Google Earth Engine (GEE). The process includes setting up the environment, defining cloud and cloud shadow components, building a cloud-free composite, and visualizing the results using Folium.

---

## Setup

1. **Initialize the Environment**:
   - Import necessary libraries, including Earth Engine (`ee`) and Geopandas.
   - Authenticate and initialize the Earth Engine API.
   - Mount Google Drive to access files.

2. **Define Parameters**:
   - Set the start and end dates for the image collection.
   - Specify the path to the shapefile defining the Area of Interest (AOI).

---

## Data Preparation

### Assemble Cloud Mask Components

1. **Define Collection Filter and Cloud Mask Parameters**:
   - Parameters like AOI, start and end dates, cloud filter percentage, cloud probability threshold, near-infrared reflectance threshold, cloud projection distance, and buffer distance are defined to filter the Sentinel-2 image collection and identify clouds and shadows.

2. **Build Sentinel-2 Collection**:
   - Load the Sentinel-2 surface reflectance and cloud probability collections.
   - Filter the collections by AOI and date.
   - Join the filtered collections on the `system:index` property to combine SR and cloud probability images.

3. **Define Cloud Mask Component Functions**:
   - Add cloud probability and cloud mask as bands to an image.
   - Identify dark pixels, project cloud shadows, and define the cloud-shadow mask by combining cloud and shadow components.

---

## Model Training and Evaluation

### Visualize and Evaluate Cloud Mask Components

1. **Define Visualization Functions**:
   - Use Folium to create an interactive map.
   - Define methods to display Earth Engine image tiles on the map.

2. **Display Cloud and Cloud Shadow Components**:
   - Mosaic the image collection.
   - Prepare and display various mask components like clouds, shadows, dark pixels, probability, and cloudmask.

3. **Evaluate Mask Components**:
   - Use interactive maps to toggle layers on and off, evaluating the effectiveness of different parameters.
   - Experiment with different values for cloud probability threshold, NIR threshold, cloud projection distance, and buffer to optimize the mask for different conditions.

---

## Apply Cloud and Cloud Shadow Mask

1. **Redefine Collection Filter and Cloud Mask Parameters**:
   - Adjust parameters to create a more aggressive mask, aiming to ensure a cloud-free composite by increasing the cloud projection distance and buffer, while decreasing the cloud probability threshold.

2. **Build a New Sentinel-2 Collection**:
   - Reassemble the collection with the updated parameters.

3. **Define Mask Application Function**:
   - Apply the cloud mask to each image in the collection, updating the mask for reflectance bands.

4. **Process the Collection**:
   - Map the cloud and shadow mask function over the collection.
   - Apply the mask and reduce the collection by taking the median of the images to create a cloud-free composite.

---

## Visualization

1. **Display the Cloud-Free Composite**:
   - Use Folium to create an interactive map.
   - Add the cloud-free composite to the map and display it.

By following these steps, you can effectively mask clouds and cloud shadows in Sentinel-2 data using Earth Engine and `s2cloudless`, producing a cloud-free composite image suitable for further analysis. This approach leverages the power of Earth Engine for large-scale geospatial data processing and visualization.
