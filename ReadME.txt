Urban Change Detection in Tirana (2000–2025)

Workflow and Datasets


1. Project Description
This repository contains all spatial datasets and the full processing workflow used for the analysis and visualization of urban changes in Tirana, Albania, from 2000 to 2025. 
Only Tirana has been analyzed for urban changes, while administrative boundaries for Western Balkan countries and selected European countries have been included solely for visualization purposes.



2. Data Sources & Download Links
2.1 Administrative Boundaries
Source: OSM Boundaries
Main link: https://osm-boundaries.com/
Boundaries were downloaded using the following filters:
•	Admin Level: Min 2, Max 2
•	Boundary: administrative
•	Format: GeoJSON
•	SRID: 4326
Country-specific download links:
•	Bosnia and Herzegovina:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-2528142&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
•	Kosovo:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-2088990&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
•	North Macedonia:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-53293&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
•	Montenegro:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-53296&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
•	Serbia:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-1741311&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
•	Albania (North/Central/South):
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-53292&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
•	For visualization only (not analyzed):
o	Slovenia:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-192307&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
o	Bulgaria:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-186382&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
o	Hungary:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-21335&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
o	Italy:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-365331&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
o	Turkey:
https://osm-boundaries.com/api/v1/download?db=osm20250407&osmIds=-174737&recursive=true&minAdminLevel=2&maxAdminLevel=2&boundary=administrative&format=GeoJSON&srid=4326
For Tirana Municipality:
•	Downloaded from the National Geoportal (ASIG, login required):
https://geoportal.asig.gov.al/
Note: Administrative boundaries for Western Balkan countries and the additional European countries above were used exclusively for map visualization and context, not for urban change analysis.


2.2 Urban Atlas and CORINE Datasets
•	Urban Atlas 2018: https://land.copernicus.eu/en/products/urban-atlas/urban-atlas-2018
•	Urban Atlas 2012: https://land.copernicus.eu/en/products/urban-atlas/urban-atlas-2012
•	Urban Atlas 2006: https://land.copernicus.eu/en/products/urban-atlas/urban-atlas-2006
•	CORINE Land Cover 2006: https://land.copernicus.eu/en/products/corine-land-cover/clc-2006
Processing:
•	A new field “Categories” was created.
•	All original classes were merged into: Agriculture, Green Areas, Urban, Water, Infrastructure, Other (see details below).
•	The category assignment was:
	Agriculture: arable land (annual crops), pastures
	Green Areas: forests, green urban areas, herbaceous vegetation, sports and leisure facilities
	Urban: construction sites, continuous urban fabric, discontinuous urban fabric (low/medium/dense), isolated structures
	Water: water, wetlands, open spaces with no vegetation (e.g., beaches)
	Infrastructure: other roads and associated land, railway and associated land
	Other: land without current use, mineral extraction and dumps sites


2.3 Raster Data

•	Sentinel-2 Data – 2016, 2020, 2025:
https://browser.dataspace.copernicus.eu/?zoom=5&lat=50.16282&lng=20.78613&themeId=DEFAULT-THEME&visualizationUrl=U2FsdGVkX194bdGCUurFkxUr54Ft4ESY3wva3XGV86Kb0UqZoeC9240TjwHRDGXMginmAbBxtjvHh0XYzn7t3HTYnmVf%2FpOBCZZ6lBGRV9HDj15%2Bl3VfClxW4xFA9omg&datasetId=S2_L2A_CDAS&demSource3D=%22MAPZEN%22&cloudCoverage=30&dateMode=SINGLE
•	Landsat Data – 2000, 2006, 2010:
https://earthexplorer.usgs.gov/
•	NDVI/NDBI indices were calculated for each year as described below.



3. Data Organization GPK
•	/Vector_data/
o	Urban Atlas 2012 with categories
o	Urban Atlas 2018 with categories
o	UA2006_CLC with categories

o	Administrative boundaries:
	Western_Balkans (used for visualization)
	Tirana Municipality (used for analysis)
	Europe_Countries_Visualization

•	/Raster_data/
o	Sentinel (all used years)
o	Landsat (all used years)
o	NDVI & NDBI (all years)

•	/MOLUSCE/
o	MOLUSCE input/output data (for change modeling)
•	/Documentation/

o	Maps for final visualization
•	/Excel_Charts/
o	Charts showing percent share by land cover class



4. Processing Workflow
1.	Download boundaries from OSM Boundaries using the above filters. Merge for Western Balkans if necessary (to exclude water areas, North/Central/South for Albania).
2.	Download Urban Atlas & CORINE datasets for 2006, 2012, 2018. Reclassify all classes into six main categories as above.
3.	Download satellite imagery (Sentinel-2, Landsat) for the relevant years.
4.	Calculate NDVI and NDBI indices (see calculation section below for formulas and band selection).
5.	Prepare data for MOLUSCE (change modeling in QGIS).
6.	Perform graphical analysis: Aggregate area (ha/km²), compute percent share per category, and visualize results in Excel.



5. Calculation of Spectral Indices (Formulas & Bands)
Landsat 5
•	NDVI (Normalized Difference Vegetation Index):
NDVI = (Band 4 - Band 3) / (Band 4 + Band 3)
o	Band 4 = Near-Infrared (NIR): 0.76–0.90 µm
o	Band 3 = Red: 0.63–0.69 µm
•	NDBI (Normalized Difference Built-up Index):
NDBI = (Band 5 - Band 4) / (Band 5 + Band 4)
o	Band 5 = Shortwave Infrared (SWIR): 1.55–1.75 µm
o	Band 4 = Near-Infrared (NIR): 0.76–0.90 µm
Sentinel-2
•	NDVI:
NDVI = (Band 8 - Band 4) / (Band 8 + Band 4)
o	Band 8 = Near-Infrared (NIR): 0.842 µm
o	Band 4 = Red: 0.665 µm
•	NDBI:
NDBI = (Band 11 - Band 8) / (Band 11 + Band 8)
o	Band 11 = Shortwave Infrared (SWIR): 1.610 µm
o	Band 8 = Near-Infrared (NIR): 0.842 µm



6. Reproducibility
•	All datasets are open or free for academic use.
•	The workflow is documented for full reproducibility.
•	If you use this workflow or data, please cite the original sources and this documentation.



7. References
•	OSM Boundaries
•	Copernicus Urban Atlas 2018
•	Copernicus Urban Atlas 2012
•	Copernicus Urban Atlas 2006
•	Copernicus CORINE Land Cover 2006
•	USGS EarthExplorer
•	Copernicus Data Space
•	ASIG Geoportal

