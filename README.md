# DATA 512: Course Project

This is an ongoing project that tries to answer the question: What are the estimated wildfire impacts on Grand Junction, Colorado for the last 60 years? We also answer these following questions.
1. Produce a histogram showing the number of fires occurring every 50 mile distance from your assigned city up to the max specified distance.
2. Produce a time series graph of total acres burned per year for the fires occurring in the specified distance from your city.
3. Produce a time series graph containing your fire smoke estimate for your city and the AQI estimate for your city.

## Sources of Data:
1. [USGS Wildland Fire Combined Dataset](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). This dataset was collected and aggregated by the US Geological Survey. The dataset is relatively well documented. Fire polygons are available in ArcGIS and GeoJSON formats.

2. [US EPA Air Quality System API](https://aqs.epa.gov/aqsweb/documents/data_api.html)

### Pre requisite:
In order to work with this code, you would need to download the data from the Source mentioned above from the USGS website. We would be working with the file titled `USGS_Wildland_Fire_Combined_Dataset.json`, and you can safely discard the rest for running the project. Paste the file in the data/GeoJSON_Exports/ folder.

## Repository Structure

1. data - Contains the intermediary data files that are used to create visuals and further analyse the data.
2. src - contains code for data extraction, analysis and visual creation.
3. images - Contains images of the outputs for the questions asked.



## Outputs

The analysis for now has led into 2 parts
1. Creating a basic smoke impact model and comparing that with the AQI data from EPA
2. Creating basic visuals like the following:



## References:
1. Welty, J.L., and Jeffries, M.I., 2021, Combined wildland fire datasets for the United States and certain territories, 1800s-Present: U.S. Geological Survey data release, https://doi.org/10.5066/P9ZXGFY3.
2. Codebase of Prof David W. McDonald for data extraction and processing from the API: [Link](https://drive.google.com/file/d/1bxl9qrb_52RocKNGfbZ5znHVqFDMkUzf/view)