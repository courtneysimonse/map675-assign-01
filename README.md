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
```shell
>ogrinfo -so Countywide_Parks__Green_Spaces\Countywide_Parks__Green_Spaces.shp Countywide_Parks__Green_Spaces
INFO: Open of `Countywide_Parks__Green_Spaces\Countywide_Parks__Green_Spaces.shp'
      using driver `ESRI Shapefile' successful.

Layer name: Countywide_Parks__Green_Spaces
Geometry: Polygon
Feature Count: 4392
Extent: (1216700.624978, 265175.250028) - (1563015.374932, 604508.562501)
Layer SRS WKT:
PROJCS["NAD83 / Ohio South (ftUS)",
    GEOGCS["NAD83",
        DATUM["North_American_Datum_1983",
            SPHEROID["GRS 1980",6378137,298.257222101,
                AUTHORITY["EPSG","7019"]],
            TOWGS84[0,0,0,0,0,0,0],
            AUTHORITY["EPSG","6269"]],
        PRIMEM["Greenwich",0,
            AUTHORITY["EPSG","8901"]],
        UNIT["degree",0.0174532925199433,
            AUTHORITY["EPSG","9122"]],
        AUTHORITY["EPSG","4269"]],
    PROJECTION["Lambert_Conformal_Conic_2SP"],
    PARAMETER["standard_parallel_1",40.03333333333333],
    PARAMETER["standard_parallel_2",38.73333333333333],
    PARAMETER["latitude_of_origin",38],
    PARAMETER["central_meridian",-82.5],
    PARAMETER["false_easting",1968500],
    PARAMETER["false_northing",0],
    UNIT["US survey foot",0.3048006096012192,
        AUTHORITY["EPSG","9003"]],
    AXIS["X",EAST],
    AXIS["Y",NORTH],
    AUTHORITY["EPSG","3735"]]
NAME: String (80.0)
SHORT_NAME: String (80.0)
PARKTYPE: String (80.0)
COUNTY: String (80.0)
CREATOR: String (80.0)
MANAGER_NA: String (80.0)
SITE_CITY: String (80.0)
SITE_PHONE: String (80.0)
SITE_BOOK: Integer64 (10.0)
UNK_SITES: Integer64 (10.0)
COMPLETED: Integer64 (10.0)
OWNER: String (80.0)
OWNER2: String (80.0)
EST_ACRES: Integer64 (10.0)
ACRES: Real (24.15)
AGENCY: Integer64 (10.0)
RECNO: Integer64 (10.0)
LINKED: Integer64 (10.0)
CLASS: String (80.0)
SHOW: Integer64 (10.0)
DISTRICT_N: String (80.0)
OBJECTID: Integer64 (10.0)
PARK_NUMBE: Integer64 (10.0)
OWNERSHIP: String (80.0)
VERIFIED: String (80.0)
SITE_ADDRE: String (80.0)
SITE_ZIPCO: String (80.0)
SITE_COMME: String (80.0)
STATE_NUMB: Integer64 (10.0)
PARCELID: String (80.0)
GLOBALID: String (80.0)
SHAPEAREA: Integer64 (10.0)
SHAPELEN: Integer64 (10.0)
```
I then converted the shapefile from NAD83 to WGS84 and converted that to GeoJSON:
```shell
>ogr2ogr Countywide_Parks__Green_Spaces_4326.shp -t_srs "EPSG:4326" Countywide_Parks__Green_Spaces.shp
>ogrinfo -so Countywide_Parks__Green_Spaces_4326.shp Countywide_Parks__Green_Spaces_4326
INFO: Open of `Countywide_Parks__Green_Spaces_4326.shp'
      using driver `ESRI Shapefile' successful.

Layer name: Countywide_Parks__Green_Spaces_4326
Metadata:
  DBF_DATE_LAST_UPDATE=2019-10-21
Geometry: Polygon
Feature Count: 4392
Extent: (-85.166495, 38.714357) - (-83.938480, 39.650414)
Layer SRS WKT:
GEOGCS["WGS 84",
    DATUM["WGS_1984",
        SPHEROID["WGS 84",6378137,298.257223563,
            AUTHORITY["EPSG","7030"]],
        AUTHORITY["EPSG","6326"]],
    PRIMEM["Greenwich",0,
        AUTHORITY["EPSG","8901"]],
    UNIT["degree",0.0174532925199433,
        AUTHORITY["EPSG","9122"]],
    AUTHORITY["EPSG","4326"]]
NAME: String (80.0)
SHORT_NAME: String (80.0)
PARKTYPE: String (80.0)
COUNTY: String (80.0)
CREATOR: String (80.0)
MANAGER_NA: String (80.0)
SITE_CITY: String (80.0)
SITE_PHONE: String (80.0)
SITE_BOOK: Integer64 (10.0)
UNK_SITES: Integer64 (10.0)
COMPLETED: Integer64 (10.0)
OWNER: String (80.0)
OWNER2: String (80.0)
EST_ACRES: Integer64 (10.0)
ACRES: Real (24.15)
AGENCY: Integer64 (10.0)
RECNO: Integer64 (10.0)
LINKED: Integer64 (10.0)
CLASS: String (80.0)
SHOW: Integer64 (10.0)
DISTRICT_N: String (80.0)
OBJECTID: Integer64 (10.0)
PARK_NUMBE: Integer64 (10.0)
OWNERSHIP: String (80.0)
VERIFIED: String (80.0)
SITE_ADDRE: String (80.0)
SITE_ZIPCO: String (80.0)
SITE_COMME: String (80.0)
STATE_NUMB: Integer64 (10.0)
PARCELID: String (80.0)
GLOBALID: String (80.0)
SHAPEAREA: Integer64 (10.0)
SHAPELEN: Integer64 (10.0)
>ogr2ogr -f "GeoJSON" cincinnati-parks.json Countywide_Parks__Green_Spaces\Countywide_Parks__Green_Spaces_4326.shp
```
