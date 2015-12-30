# Tenerife
Data and analysis script (MatLab) for a university project linking geodiversity to endemic vascular plant diversity.

# Project
Our methodology consisted of a fieldwork and a GIS part, followed by a statistical data analysis. 
During GIS work, prior to fieldwork, we prepared data layers of thematic data available (soil map, geological map), and chose our fieldwork locations to ensure a good cover of the geological and topographical variability in our specific area. We derived land surface parameters from a DTM. Land surface parameters are terrain model derivatives such as slope, curvature, and additional measures such as openness of the topography. 

During out fieldwork, our aim was to map species diversity as well as biotope diversity. Mapping biotopes in the field is nearly impossible even with expert knowledge of local plants. Therefor we adopted a stratified sampling strategy, which we calling mapping of geo-vegetation units.  Geomorphological units were delineated in the field, and subdivided into geomorphological subunits, or topographical subunits until patches with a uniform vegetation cover were obtained. This we used as a substitute for biotope mapping. In each geovegetation unit a fieldform was filled in with a characterization of abiotic conditions and a species count of endemic plant species only. Initially photographs were used to store the species that could not be identified immediately, these were later identified with the help of an expert.

Afterwards,  our map containing rasters of LSP data and thematic polygon maps with GVUs, geological units and species counts per GVU were gridded by overlaying our fieldwork plots with a fishnet of 200x200m cells in ArcMap. Each fishnet polygon got several attributes calculated from the GD-index input data, and a species and biotope count (GVU count), mean value elevation, standard dev elevation. Main geological unit, number of geological units. 

As mentioned earlier, we used a stratified approach, identifying main geomorphological units in the field, and subdividing them I into geomorphological subunits. For instance, a barranco can consist of a barranco floor, a barranco slope and several terraces, each with distinct vegetation. Moreover, additional subdivisions may be made based on activity of a slope (active part/nonactive part), topographical aspect, etc. For instance, a lava plateau was identified that had consistent species composition all over the unit, and a Barranco with several distinct biotopes. The barranco was subdivided into a barranco floor, and  barranco slopes and further divided based on aspect until consistent GVU were obtained.

Our methodology of selecting several field plots has to be upscaled of course. We propose that the upscaling is set up in a stratified and hierarchical way. By selecting three plots in our greater area, we could upscale our methods to our greater area, which was step 1. And we propose that first, several additional plots are selected in the Corona Forestal first, with different altitudes, aspects, geology, etc, so that our methodology can first be upscaled to the entire corona forestall. Then, other vegetation zones of Tenerife can be analyzed in a similar way and finally the methodology can be upscaled to the whole of Tenerife, and perhaps even other Canary Islands. 

# Data File
Contains data for each fishnet cell generated in ArcMap in csv format, semicolor separator.

*DEM* (Altitude).	Land Surface Parameter (LSP)	-	Centro Nacional de Información Geográfica (2009).	5m resolution
*Slope	LSP	- The maximum rate of change with neighbouring cells [degrees]	dervied from DEM. Calculated with ArcGIS Slope Tool from Spatial Analyst toolbox. Average and standar deviation per fishnet cell.
*Aspect.	LSP. - 	The compass direction of the neighbouring cell with the maximum rate of change with input cell [degrees] dervied from DEM. Calculated with ArcGIS Aspect Tool from Spatial Analyst toolbox. Average and standar deviation per fishnet cell.
*Curvature.	LSP.	- Second derivative of input raster within neighbouring cells [-] derived from	DEM. Calculated with ArcGIS Slope Tool from Spatial Analyst toolbox. Average and standar deviation per fishnet cell.
*Topographic Openness.	LSP. -	Mean of above-surface zenith along each azimuth up to specified radius. [degrees]	derived from DEM. Calculated using a script from Anders et al., (2011)., based on Yokoyama et al. (2002).	Calculated on 25m radius. Average and standar deviation per fishnet cell.
*Flow Accumulation.	LSP.	Accumulated number of all cells flowing into each downslope cell in the output raster [nr. of cells]	derived from DEM. Calculated with the ArcGIS Flow Direction and Flow Accumulation tools from the hydrological toolbox. Average and standar deviation per fishnet cell.
*Solar Radiation.	LSP.	Based on hemispherical viewshed algorithms. [WH/m^2]	derived from DEM. Calculated using the ArcGIS Area Solar Radiation tool from the Spatial Analyst toolbox. Average and standar deviation per fishnet cell.
*Geological units.	Thematic Data	-	Instituto Geológico y Minero de España (2010).	Scale: 1:50,000. Count per cell
*GEOMORPH - geomorphological units present in a fishnet cell, recorded during fieldwork.
*SPECIES - count of endemic vascular plants per fishnet cell, recorded during fieldwork. 

Analysis:
MatLab script, provided as .txt
Analyzes correlation between predictor variables (the LSPs and thematic data), and the biodiversity expressed as the number of GVUs and Species within a grid
