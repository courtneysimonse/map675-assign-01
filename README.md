# Assignment #1

# Data
## Data Sources

For this assignment we used data sets from a European country, the Netherlands.
The Netherlands is divided into the following administrative boundaries (Land-, Province- and Municipal borders). We used the administrative boundaries toghter with the railways and train stations. https://www.imergis.nl/htm/opendata.htm.
Shape files and geopackage were available. The geopackages were opened in QGIS and saved as shape files.

![Landgrens](/images/Ned_Bestuurlijkegrenzen.jpg "administrative boundaries")


### Courtney's Data Process
Cincinnati-owned Properties  
The Cincinnati Owned Properties layer displays all properties owned or leased by the City of Cincinnati throughout Hamilton County:
 https://data-cagisportal.opendata.arcgis.com/datasets/cincinnati-owned-properties


```shell
>mkdir Cincinnati_Owned_Properties
>tar -xvf "Cincinnati_Owned_Properties.zip" -C Cincinnati_Owned_Properties/
x Cincinnati_Owned_Properties.prj
x Cincinnati_Owned_Properties.dbf
x Cincinnati_Owned_Properties.shp
x Cincinnati_Owned_Properties.shx
x Cincinnati_Owned_Properties.xml
x Cincinnati_Owned_Properties.cpg
  ```
Greater Cincinnati Parks and Greenspaces  
Parks and Green Space of Hamilton, Clermont, Warren, Butler, Campbell, Greene, Kenton, Dearborn, Boone, Montgomery, Greene, Clinton, and Preble counties:  
https://data-cagisportal.opendata.arcgis.com/datasets/f41afa1a4fa94e7f99c7cbc6fe75484b_2  

```shell
>mkdir Countywide_Parks__Green_Spaces
>tar -xvf "Countywide_Parks__Green_Spaces.zip" -C Countywide_Parks__Green_Spaces/
x Countywide_Parks__Green_Spaces.cpg
x Countywide_Parks__Green_Spaces.shx
x Countywide_Parks__Green_Spaces.dbf
x Countywide_Parks__Green_Spaces.prj
x Countywide_Parks__Green_Spaces.shp
```
