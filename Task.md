
## Interpolation

### Data

The airquality dataset (luftqualitaet.gpkg) contains measurements of nitrogen dioxide NO₂ from 2015 for 97 monitoring sites in Switzerland. Nitrogen dioxide is produced when fuels and combustibles are burned, especially at high combustion temperatures, with road traffic being the main source. You can find more information on this here.

### Exercise 1: IDW

Use the function gstat::idw to interpolate the NO₂ values using the inverse distance weighted method.

Note
The function idw needs following inputs: formula, locations and newdata

formula: For ordinary, simple kriging use the formula z~1 where z is the column name of the dependent variable
locations: A sf object with the locations of the dependent variable
newdata: A sf object with the locations for which the dependent variable should be calculated. Can be created with sf::st_make_grid. The cellsize arugument determins the resolution of the resuting dataset.
Optional arguments:

maxdist: Maximum distance to which measurements should be considered
nmin /nmax: Minimum and maxximum number of measurements to consider
idp the inverse distance weighting power
Play around with maxdist, nmin /nmaxand idp. Convert the resulting sf object to a raster (find out how!) and visualize the result.

### Exercise 2: Nearest Neighbour

Another simple option for interpolation is the nearest neighbour approach, that we can recreate using voronoi polygons. Use the approach described in Exercise 2: Voronoi to create voronoi polygons. Turn the resulting sfc object to sf using st_as_sf, then use st_join to add the measured NO2 values the polygons.

Visualize the result.

## Density Estimation

### Data

The data set rotmilan.gpkg originates from a larger research project of the Sempach Ornithological Institute which can be accessed via the platform movebank platform (see Scherler 2020). This is a single individual that has been fitted with a transmitter since 2017 and is travelling across the whole of Central Europe. In this exercise, we only work with the data points that were recorded in Switzerland. If you would like to analyse the entire data set, you can download it via the Movebank link.

### Exercise 1: Kernel Density Estimation

To calculate the a 2D Kernel over our data, use the function density from the R package spatstat.

Note
x, the point pattern, needs to be of class ppp. Use the function as.ppp to convert our red kite data
eps is an argument passed on to as.maks to determine the output resolution / pixel size. Choose a reasonable size (not too pixelated, not to slow in computing)
You can convert the output (of class im) to a raster using the function terra::rast
Try out different options for sigma and choose a reasonable parameter
Try different functions to choose sigma: bw.diggle, bw.CvL, bw.scott and bw.ppl.

### Exercise 2: Voronoi

Thiessen polygons offer an alternative for visualising differences in the density distribution of point data sets. You can create these using the function sf::st_voronoi.

Note
You have to combine the individual points to MULTIPOINT using the function sf::st_union.
st_voronoi takes an envelope argument, however this only takes effect when it is larger than the default envelope. Use sf::st_intersection to clip your output to the boundary of switzerland.