# NR427final
final projected for NR427
This jupyter notebook takes the following data:

Hosted online
- Colorado streams
- Colorado lakes
- Colorado watersheds

From zipfiles on the internet
- BAER burn severity info (109.8 mb)
- DEM for area of interest in Colorado (57.3mb)
- slope geojson (688 kb)

The script identifies areas of high erosion risk, which is defined in this script as areas that burned at high severity occurring on slopes of 30% or steeper.  The script refers to this area as the “Danger Zone.”  The script then identifies streams that flow through these areas, watersheds containing the Danger Zone, lakes within these watersheds.

The script creates 3 products:
- .csv file of the largest lakes (> 10 hectares surface area) in watersheds that are at risk
- .csv file showing the total amount of Danger Zone area (in hectares) within each watershed
- .pdf of a nicely formatted plot showing Danger Zone overlaid on watersheds, along with streams that flow through it and lakes within the relevant watersheds

Note:
- this script can take ~5 minutes to run (at least according to my latest pass)
- loading in some of those online layers takes a minute!
- run time will be affected by internet speed, since we are both loading and downloading data
- while I did successfully reclassify and polgyonize burn severity data, i ran into some roadblocks doing the same for slope raster (once I created that from DEM).  i was able to create slope and reclassify it, but polygonization failed.  my workaround was creating my own slope polygon and hosting the GeoJSON file online.  *However*, i included all of the code to download the zipped DEM from online, create slope, reclassify slope into binary (steep slopes, other slopes).  at that point, i download and unzip the slope polygon, and proceed with selecting out steep areas.  so… i really did every step, just got hung up on polygonization for some reason.

Please also note that I definitely borrowed some tips, tricks and adapted various chunks of code to help me with some of the more complex processes (attribution is given to the appropriate sources throughout).

A few things that I think are neat:

1. this script uses data exclusively from online sources.  no hardcoding.  no files to send you besides the notebook and this readme 
2. this script eschews arcpy and AGOL in favor of open source python libraries
3. rather than using the hosted burn severity polygon you provided us with, I made my own by taking the dNBR .tif file from the BAER data online, reclassifying it into four burn severity categories (unburned, low, moderate, high) and turned it into a polygon, and then identified “high severity” areas

enjoy!
jesse
