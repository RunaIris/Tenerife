# Tenerife
Data and analysis script (MatLab) for a university project linking geodiversity to endemic vascular plant diversity. The project took place in September and October 2015, within the course "Vulnerability of Geo-Ecosystems" at the University of Amsterdam, under supervision of Dr. Harry Seijmonsbergen and Dr. Kenneth Rijsdijk. The project was carried out by master students Ben van Meeteren, Joost Dalmijn and Runa Magnusson.

The aim of the project was to create a Geodiversity Index based on widely available Terrain Data and existing Thematic Maps with predictive capacity for biodiversity. Biodiversity is difficult and costly to measure in the field, thus, the use of a Geodiversity Index as a indicator for finescale Biodiversity could facilitate the mapping of Biodiversity over a large extent on a fine scale. This in turn could be used as a tool in policy making and conservation priorization. We tested out methodology in the southern part of the Corona Forestal National Park on Tenerife.

### Project
Our methodology consisted of a fieldwork and a GIS part, followed by a statistical data analysis. 
During GIS work, prior to fieldwork, we prepared data layers of thematic data available (soil map, geological map), and chose our fieldwork locations to ensure a good cover of the geological and topographical variability in our specific area. This was done by selecting 3 600x600m plots, and one 200x600m validation plot with diverse height, topography and geology. We derived land surface parameter maps from a Digital Terrain Model (DTM). Land surface parameters are terrain model derivatives such as slope, curvature, and additional measures such as openness of the topography. 

During our fieldwork, our aim was to map species diversity as well as biotope diversity. Mapping biotopes in the field is nearly impossible even with expert knowledge of local plants. Therefore we adopted a stratified sampling strategy, which we called mapping of geo-vegetation units (GVUs).  Main geomorphological units were delineated in the plots, and subdivided into geomorphological subunits, or topographical subunits until patches with a uniform vegetation cover were obtained. For instance, a barranco can consist of a barranco floor, a barranco slope and several terraces, each with distinct vegetation. Moreover, additional subdivisions may be made based on activity of a slope (active part/nonactive part), topographical aspect, etc. For instance, a lava plateau was identified that had consistent species composition all over the unit, and a Barranco with several distinct biotopes. The barranco was subdivided into a barranco floor, and  barranco slopes and further divided based on aspect until consistent GVU were obtained. These GVUs we used as a substitute for biotope mapping. In each geovegetation unit a fieldform was filled in with a characterization of abiotic conditions and a species count of endemic plant species only. Initially photographs were used to store the species that could not be identified immediately, these were later identified with the help of an expert, Dr. Gerard Oostermeijer.

Afterwards,  our map containing rasters of LSP data and thematic polygon maps with GVUs, geological units and species counts per GVU were gridded by overlaying our fieldwork plots with a fishnet of 200x200m cells in ArcMap. Each fishnet polygon got several attributes calculated from the GD-index input data, and a species and biotope count (expressed as GVU count). LSP derivatives included mean and standard deviation of each LSP per cell (e.g. mean value elevation, standard dev elevation). Thematic data were expressed as main feature per cell and number of features per cell (e.g. main geological unit, number of geological units). This yielded the dataset present in this repository, of attributes per 200x200m fishnet cell. Two methods were adopted to calculate a Geodiversity Index (GD index) predictive for biodiversity from the Terrain- and Thematic predictor variables, explained in the paragraph "Analysis".

### Data File
This repository contains a file called "data", in .txt format. It contains data for each fishnet cell generated in ArcMap and converted to csv with semicolor separator.

**DEM** (Altitude).	Land Surface Parameter (LSP)	-	Centro Nacional de Información Geográfica (2009).	5m resolution
- Mean Altitude per cell
- Standard Deviation of Altitude per cell

**Slope**	LSP	- The maximum rate of change with neighbouring cells [degrees]	dervied from DEM. Calculated with ArcGIS Slope Tool from Spatial Analyst toolbox. Average and standar deviation per fishnet cell.
- Mean Slope angle per cell
- Standard Deviation of Slope angle per cell

**Aspect**	LSP. - 	The compass direction of the neighbouring cell with the maximum rate of change with input cell [degrees] dervied from DEM. Calculated with ArcGIS Aspect Tool from Spatial Analyst toolbox. Average and standar deviation per fishnet cell.
- Mean Aspect per cell
- Standard Deviation of Aspect per cell

**Curvature**	LSP.	- Second derivative of input raster within neighbouring cells [-] derived from	DEM. Calculated with ArcGIS Slope Tool from Spatial Analyst toolbox. Average and standar deviation per fishnet cell.
- Mean Curvature per cell
- Standard Deviation of Curvature per cell

**Topographic Openness**	LSP. -	Mean of above-surface zenith along each azimuth up to specified radius. [degrees]	derived from DEM. Calculated using a script from Anders et al., (2011)., based on Yokoyama et al. (2002).	Calculated on 25m radius. Average and standar deviation per fishnet cell.

**Flow Accumulation**	LSP.	Accumulated number of all cells flowing into each downslope cell in the output raster [nr. of cells]	derived from DEM. Calculated with the ArcGIS Flow Direction and Flow Accumulation tools from the hydrological toolbox. Average and standar deviation per fishnet cell.
- Mean Flow Accumulation per cell
- Standard Deviation of Flow Accumulation per cell

**Solar Radiation**	LSP.	Based on hemispherical viewshed algorithms. [WH/m^2]	derived from DEM. Calculated using the ArcGIS Area Solar Radiation tool from the Spatial Analyst toolbox. Average and standar deviation per fishnet cell.
- Mean Solar radiation per cell
- Standard Deviation of Solar Radiation per cell

**Geological units**	Thematic Data	-	Instituto Geológico y Minero de España (2010).	Scale: 1:50,000. Count per cell
- Count of Geological Units
- Main Geological Unit (highest % areal coverage)

**GEOMORPH** geomorphological units present in a fishnet cell, recorded during fieldwork.
- Count of Geomorphological Units
- Main Geomorphological Unit (highest % areal coverage)

**SPECIES** count of endemic vascular plants per fishnet cell, recorded during fieldwork. 

**GVU Count** count of GVUs per fishnet cell, recorded during fieldwork

### Analysis
Our statistical analysis, used to develop a GD index predictive of biodiversity, was carried out in MatLab. The code can be found in this repository as a MatLab script, provided in .txt format.

This script analyzes correlation between predictor variables (the LSPs and thematic data), and the biodiversity. It does so both for biodiversity expressed as Species per cell and number of Biotopes (GVUs) per cell. Moreover, it does so using two distinct methodologies. One methodology is the fitting of a General Linear Model (GLM), the other is the scaling and ranking of predictor variables to generate a compound, scaled and ranked GD "score" that is fitted to the biodiversity data using polynomial fitting.

For both methods alike, first, each predictor variable is tested for correlation with the two output variables. Only those with a significant correlation are kept for later analyses. Moreover, some variables are omitted because of collinearity, based on the Variance Inflation factor.

GLM method:
Several possible linear models were generated, by using forward selection, backward selection and manual bidirectional selection. Moreover, a full model containing all significant predictors was generated for comparison. The performance of these models was assessed using Leave-One-Out Crossvalidation (LOOCV). The best performing models were analysed using additional plot diagnostics (distribution of residuals, cook's distance..). 

Scaling and Ranking Method:
All significant predictor variables were scaled from 0 to 1. For continous data (LSP-derived), this was done simply by scaling based on maximum and minimum values. Of course, in cases where a negative correlation was observed from the initial correlation scatterplots generated in analysis step one, the scaled predictor variables were multiplied by -1. For Thematic data, this was done based on a hypothetical relation between this thematic variable and biodiversity (based on the correlation found in the first analysis step). So for instance, a "Lava Flow" location could get a score of 0.1 while a Barranco could get a score of 0.9. Afterwards, all scaled predictors were averaged to create a GD index based on scalink and ranking, and a correlation between this GD index and biodiversity was generated. Then, polynomials were fitted with this GD index as predictor, and the biodiversity variables as response, to see whether higher order polynomials significantly improved the fit between this GD index and biodiversity. This however did not appear to be the case and a linear relation seemed to exist between the scaled and ranked GD index and biodiversity.

Our methodology of selecting several field plots has to be upscaled of course. We propose that the upscaling is set up in a stratified and hierarchical way. By selecting three plots in our greater area, we could upscale our methods to our greater area, which was step 1. And we propose that first, several additional plots are selected in the Corona Forestal first, with different altitudes, aspects, geology, etc, so that our methodology can first be upscaled to the entire corona forestall. Then, other vegetation zones of Tenerife can be analyzed in a similar way and finally the methodology can be upscaled to the whole of Tenerife, and perhaps even other Canary Islands. 
