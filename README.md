# Wildfire and Smoke impact Analysis in Grand Junction, CO.

Wildfires have increasingly become a pervasive and pressing issue, impacting not only the immediate areas engulfed in flames but also extending their repercussions across vast distances. As communities grapple with the far-reaching consequences of these infernos, the analysis presented in this report delves into a critical nexus between wildfire-induced smoke exposure and its profound implications on respiratory health.

This analysis aims to bridge the gap in understanding the interplay between wildfire-derived smoke, air quality indices, and the incidence of respiratory diseases, specifically in the city of Grand Junction, Colorado. It seeks to unravel the complexities of this relationship, shedding light on the direct and indirect effects of prolonged exposure to wildfire smoke on respiratory health. By doing so, it aspires to provide actionable insights and potential strategies to mitigate the adverse impacts faced by our community.

The importance of this analysis is underscored by its potential to inform public policy, community preparedness, and health interventions aimed at safeguarding the populace against the insidious threat posed by wildfire smoke. It not only unravels the intricate connections between environmental factors and human health but also lays the groundwork for proactive measures to protect vulnerable populations and enhance the resilience of our community in the face of these environmental challenges.

You can find a comprehensive report in the `data/Project Report.pdf`. This document elaborates on the project's methodology and provides insights into the extracted respiratory-based mortality data.

A bried analysis on the wildfire and AQI data can be viewed in the document `document/Capstone_Part 1_ Document.pdf`. This addresses the following questions:
1. Produce a histogram showing the number of fires occurring every 50 mile distance from your assigned city up to the max specified distance.
2. Produce a time series graph of total acres burned per year for the fires occurring in the specified distance from your city.
3. Produce a time series graph containing your fire smoke estimate for your city and the AQI estimate for your city.



## Repository Structure

1. data - Contains the intermediary data files that are used to create visuals and further analyse the data.
2. src - contains code for data extraction, analysis and visual creation. `src/Data Acquisition.ipynb` contains steps taken to obtain data from the USGS JSON file and from the EPA API. `src/Building Smoke estimates.ipynb` builds upon the data and creates an initial smoke estimate and then attempts to fit a model to the created smoke estimate. Finally the `src/Visualizations.ipynb` contains the steps taken to create the visuals that are given as questions in the assignment. The final outputs are stored in the `images` folder.  Finally, the analysis on mortality vs smoke estimate can be looked in `src/Smoke Effects on Mortality.ipynb`.It is helpful to visit the files in this order.
3. images - Contains images of the outputs for the questions asked in Part 1 of the project. They can also be read about in `document/Capstone_Part 1_ Document.pdf`.


## Data Sources & Descriptions:

This section provides an overview of the input data along with their sources:

1. [USGS Wildland Fire Combined Dataset](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81): A trove of information meticulously collected and aggregated by the US Geological Survey. The dataset, available in both ArcGIS and GeoJSON formats, unveils the contours of fire polygons with comprehensive documentation. The data should be placed under `data/GeoJSON_Exports/`.(Read the pre requisite section for more information). Below is a detailed breakdown of the data fields within this dataset:

| NAME | DTYPE | DESCRIPTION |
| ----------- | ----------- | ----------- |
| OBJECTID | Integer | Unique identification for the polygon and it's attributes |
| USGS_Assigned_ID | Integer | Assigned unique identification for the polygon and it's attributes. Used to provide consistency if parts of the dataset are exported or the OBJECTID is otherwise changed |
| Assigned_Fire_Type | String | Based on the fire polygon(s) used to create this fire feature what is the type assigned to this fire? If more than one type was assigned to a combined polygon, the assigned fire type was assigned in the following order of dominance: Wildfire, Likely Wildfire, Unknown - Likely Wildfire, Prescribed Fire, Unknown - Likely Prescribed Fire |
| Fire_Year | Integer | The calendar year when the dataset creators determined the fire occurred |
| Fire_Polygon_Tier | Integer | The tier from which the fire polygon was generated. One or more polygons within the tier could be combined to create the fire polygon |
| Fire_Attribute_Tiers | String | All fire tiers that contributed attributes to the fire feature. A list of all tiers where a polygon intersects the current fire perimeter in space and time |
| GIS_Acres | Float | The GIS calculated acres of the fire polygon calculated by using the Calculate Geometry tool in ArcGIS Pro |
| GIS_Hectares | Float | The GIS calculated hectares of the fire polygon calculated by using the Calculate Geometry tool in ArcGIS Pro |
| Source_Datasets | String | All of the original source datasets that contributed to either the polygon or the attributes. Each dataset has the number of polygons contributed listed in parentheses after the dataset name |
| Listed_Fire_Types | String | Each fire type listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire type are in parentheses after the fire type |
| Listed_Fire_Names | String | Each fire name listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire name are in parentheses after the fire name |
| Listed_Fire_Codes | String | Each fire code listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire code are in parentheses after the fire code |
| Listed_Fire_IDs | String | Each fire type listed in the IDs from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire ID are in parentheses after the fire ID |
| Listed_Fire_IRWIN_IDs | String | Each fire IRWIN ID listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire IRWIN ID are in parentheses after the fire IRWIN ID |
| Listed_Fire_Dates | String | Each fire date listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire date are in parentheses after the fire date |
| Listed_Fire_Causes | String | Each fire cause listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire cause are in parentheses after the fire cause |
| Listed_Fire_Cause_Class | String | Each fire cause class listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire cause class are in parentheses after the fire cause class |
| Listed_Rx_Reported_Acres | String | Each prescribed fire reported acres listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific reported acres are in parentheses after the reported acres |
| Listed_Map_Digitize_Methods | String | Each fire digitization method listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire digitization method are in parentheses after the fire digitization method |
| Listed_Notes | String | Each fire notes listed in the fires from the merged dataset that intersect this polygon in space and year. The number of features that contributed the specific fire notes are in parentheses after the fire note |
| Processing_Notes | String | Indicates that the attribute data were altered during the processing and a new attribute was indicated. It will also explain the rationale for the change. Each polygon that had an attribute changed will be listed along with a count, in parentheses indicating how many polygons had the change made to them |
| Wildfire_Notice | String | A notice present in every field that indicates the quality of the wildfire data in this dataset |
| Prescribed_Burn_Notice | String | A notice present in every field that indicates the quality of the prescribed burn data in this dataset |
| Wildfire_and_Rx_Flag | String | A text flag field indicating that the attributes from the various sources indicate that the fire was both a wildfire and a prescribed fire. This could indicate an error in assigning the fire type, a misassignment of the fire type, or that there were actually two fires that occurred in this area in the same year, one a wildfire and one a prescribed burn |
| Overlap_Within_1_or_2_Flag | String | An ArcGIS Tabulate Intersection Tool was used to identify areas that burned with >10% overlap of the current fire within 1 or 2 years of the current burn. Each fire that met that criteria was included in this attribute including it's ID, year burned, percent overlap, and acres |
| Circleness_Scale | Float | A measure of a polygon's similarity to a true circle. calculated using the Shape_Length and Shape_Area fields. Circle-ness = 4*pi*(Shape_Area/(Shape_Length * Shape_Length)). As the number approaches 1, the polygon becomes more circular |
| Circle_Flag | String | Any Circle circle-ness values >=0.98 are flagged with a 1. The remaining values are null. 1 indicates that the polygon is very circle-like and is likely incorrect. However, other values that are not flagged may still be quite circular and incorrect |
| Exclude_From_Summary_Rasters | String | Some fires in this dataset appear to be buffered circles. These were kept in the dataset to show location and approximate area. However a decision was made to exclude circular fires larger than 1 acre in size from the summary raster calculations. This field indicates whether the fire was excluded from ('Yes') or included in ('No') the summary raster calculations |
| Shape_Length | Float | Automatically calculated perimeter length in meters |
| Shape_Area | Float | Automatically calculated polygon area in square meters |

2. [US EPA Air Quality System API](https://aqs.epa.gov/aqsweb/documents/data_api.html): A nationwide repository of air sample data, encompassing meteorological insights and AQI values for diverse pollutants from an array of monitoring stations.

3. [Respiratory Disease Mortalities in the United States (1980-2014)](https://ghdx.healthdata.org/record/ihme-data/united-states-chronic-respiratory-disease-mortality-rates-county-1980-2014): This dataset, available in CSV format from the Institute for Health Metrics and Evaluation (IHME) website, chronicles mortalities caused by respiratory diseases in the United States. Maintained and hosted by IHME, it covers mortality data from 1980 to 2014 across all counties in the USA.  This is placed as the `data/IHME_USA_COUNTY_RESP_DISEASE_MORTALITY_1980_2014_COLORADO_Y2017M09D26.CSV` in this repo.

   The dataset offers comprehensive information on causes, years, sexes, and estimates such as posterior mean, 2.5th percentile, and 97.5th percentile estimates. It specifically outlines age-standardized mortality rates (deaths per 100,000 population) among various sexes and for the combined sexes for the years 1980-2014 across all counties. Included in this dataset are both string-based descriptors (measure_name, location_name, cause_name, sex, age_name, metric) and integer-based identifiers (measure_id, location_id, FIPS, cause_id, sex_id, age_id, year_id, mx, lower, upper). Importantly, the dataset is devoid of any null values across all columns, ensuring clean and comprehensive data. For further insights, a detailed description of the 16 columns is provided in the table below.

   | NAME | DTYPE | DESCRIPTION |
   | ----------- | ----------- | ----------- |
   | measure_id | Integer | Unique numeric identifier for the measure generated |
   | measure_name | String | The measure (indicator) of the estimate |
   | location_id | Integer | Unique numeric identifier for the location generated |
   | location_name | String | Location of the estimate |
   | FIPS | Integer | The Federal Information Processing Standards (FIPS) code, a unique identifier for states and counties in the United States |
   | cause_id | Integer | Unique numeric identifier for the cause of disease or injury generated |
   | cause_name | String | Cause of disease or injury of the estimate |
   | sex_id | Integer | Unique numeric identifier for the sex generated |
   | sex | String | Gender for the estimate |
   | age_id | Integer | Unique numeric identifier for the age group generated |
   | age_name | String | Age group estimated |
   | year_id | Integer | Time period of estimate |
   | metric | String | Metric/unit of measure for the estimate |
   | mx | Float | Posterior mean estimate |
   | lower | Float | 2.5% percentile estimate |
   | upper | Float | 97.5% percentile estimate |


### Intermediary data files in the data folder:

- Daily_particulate_data_Grand_Junction.csv - Contains the sub result of the daily particulate AQI data for the Stations in Grand Junction over the years.           
- Daily_gas_data_Grand_Junction.csv - Contains the sub result of the daily gaseous AQI data for the Stations in Grand Junction over the years.       
- average_top_5_aqi.csv  - the result of the calculation of AQI Estimates for the city, built during the analysis in `src/Building Smoke Estimate.ipynb`
- average_smoke_area_distance_estimate.csv - the result of the calculation of Smoke Estimates for the city, built during the analysis in `src/Building Smoke Estimate.ipynb`
- predictions_data.csv - Contains the result for the time series prediction that we did at the end of the `src/Building Smoke Estimate.ipynb`. 
- Grand_Junction_Wildfire_Features_geometry_dropped.json - This is the wildfire dataset with the polygon features dropped. This is easier to work with and load for further analysis. built during the data extraction in `src/Data Acquisition.ipynb`


## Pre requisite:
In order to work with this code, you would need to download the data from the source mentioned above from the USGS website. We would be working with the file titled `USGS_Wildland_Fire_Combined_Dataset.json`, and you can safely discard the rest for running the project. Paste the file in the `data/GeoJSON_Exports/` folder.

## Outputs

The analysis for now has led into 2 parts
1. Creating a basic smoke impact model and comparing that with the AQI data from EPA. This can be viewed at the end of `src/Building Smoke estimates.ipynb` notebook.
2. Creating visuals for the questions asked at the top of this document.



## References:
1. Welty, J.L., and Jeffries, M.I., 2021, Combined wildland fire datasets for the United States and certain territories, 1800s-Present: U.S. Geological Survey data release, https://doi.org/10.5066/P9ZXGFY3.
2. Codebase of Prof David W. McDonald for data extraction and processing from the API: [Link](https://drive.google.com/file/d/1bxl9qrb_52RocKNGfbZ5znHVqFDMkUzf/view)




