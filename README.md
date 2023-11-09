# Wildfire and Smoke impact Analysis

This is an ongoing project that tries to answer the question: What are the estimated wildfire impacts on Grand Junction, Colorado for the last 60 years? We also answer these following questions through visuals, whose results can be viewed in the document `Capstone_Part 1_ Document.pdf`.
1. Produce a histogram showing the number of fires occurring every 50 mile distance from your assigned city up to the max specified distance.
2. Produce a time series graph of total acres burned per year for the fires occurring in the specified distance from your city.
3. Produce a time series graph containing your fire smoke estimate for your city and the AQI estimate for your city.

## Sources of Data:
1. [USGS Wildland Fire Combined Dataset](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81): A trove of information meticulously collected and aggregated by the US Geological Survey. The dataset, available in both ArcGIS and GeoJSON formats, unveils the contours of fire polygons with comprehensive documentation.

2. [US EPA Air Quality System API](https://aqs.epa.gov/aqsweb/documents/data_api.html): A nationwide repository of air sample data, encompassing meteorological insights and AQI values for diverse pollutants from an array of monitoring stations.

### Pre requisite:
In order to work with this code, you would need to download the data from the source mentioned above from the USGS website. We would be working with the file titled `USGS_Wildland_Fire_Combined_Dataset.json`, and you can safely discard the rest for running the project. Paste the file in the `data/GeoJSON_Exports/` folder.

## Repository Structure

1. data - Contains the intermediary data files that are used to create visuals and further analyse the data.
2. src - contains code for data extraction, analysis and visual creation. `src/Data Acquisition.ipynb` contains steps taken to obtain data from the USGS JSON file and from the EPA API. `src/Building Smoke estimates.ipynb` builds upon the data and creates an initial smoke estimate and then attempts to fit a model to the created smoke estimate. Finally the `src/Visualizations.ipynb` contains the steps taken to create the visuals that are given as questions in the assignment. The final outputs are stored in the `images` folder. It is helpful to visit the files in this order.

3. images - Contains images of the outputs for the questions asked.

## Calculation of Smoke Estimate and Standard AQI Values

Our primary focus lies in comprehending the potential impact of wildfires on air quality. To achieve this, I employed a calculated approach to estimate the influence of fire smoke based on both the distance from the city and the extent of the area burned. This calculated estimation enables us to visually represent the evolving impact of estimated smoke over successive years.

The formula governing this estimation is expressed as follows:

`1.2 * (1- distance/1250) * (150-area/150)`

The rationale behind the chosen formula is rooted in a meticulous consideration of pertinent factors:

1. **Distance Penalization:**
   - The formula incorporates a penalization mechanism based on the maximum distance of 1250 miles for each fire. This distance is transformed into a normalized range from 0 to 1, where 0 denotes the farthest distance from the city, and 1 signifies the closest proximity. The inclusion of this distance factor serves to impose a penalty on the overall smoke creation score.

2. **Hectares Burnt Proportionality:**
   - Acknowledging the proportional relationship between the extent of hectares burned and smoke generation, the formula incorporates a normalization factor of 150. This arbitrary value, determined through a trial and error methodology, remains subject to refinement. The multiplication with this normalizing factor ensures a balanced representation of the impact of burnt area on smoke creation.

3. **Adjustment for Enhanced Range:**
   - To broaden the range and achieve a representation akin to the Air Quality Index (AQI), a scalar factor of 1.2 is added. This augmentation facilitates a more comprehensive representation of the estimated smoke, enhancing the range to encapsulate AQI-like values.



## Outputs

The analysis for now has led into 2 parts
1. Creating a basic smoke impact model and comparing that with the AQI data from EPA
2. Creating basic visuals like the following:



## References:
1. Welty, J.L., and Jeffries, M.I., 2021, Combined wildland fire datasets for the United States and certain territories, 1800s-Present: U.S. Geological Survey data release, https://doi.org/10.5066/P9ZXGFY3.
2. Codebase of Prof David W. McDonald for data extraction and processing from the API: [Link](https://drive.google.com/file/d/1bxl9qrb_52RocKNGfbZ5znHVqFDMkUzf/view)




