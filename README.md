# Assignment #1

# Data
## Data Sources

For this assignment we used data sets from a European country, the Netherlands.
The Netherlands is divided into the following administrative boundaries (Land-, Province- and Municipal borders). We used the administrative boundaries together with the railways and train stations. https://www.imergis.nl/htm/opendata.htm.
Downloaded files: (Shapefiles and geo-packages)
  1. 2019_landsgrens_kustlijn.gpkg
  2. 2019_provinciegrenzen_kustlijn.gpkg
  3. 2019_gemeentegrenzen_kustlijn.gpkg
  4. nl_imergis_kustlijn_2018.shp
  5. Top10NL_Spoorwegen.shp
  6. Top10NL_Inricht_el_station.shp

I opened the geo-packages files in QGIS and saved them as shape files.

## Using GDAL with command line GIS
### Getting Information about the shapefiles
* $ gdalinfo --version<br>
GDAL 2.4.1, released 2019/03/15

* $ ogrinfo -so Top10NL_Spoorwegen.shp Top10NL_Spoorwegen

INFO: Open of `Top10NL_Spoorwegen.shp'
      using driver `ESRI Shapefile' successful.

Layer name: Top10NL_Spoorwegen<br>
Metadata:<br>
  DBF_DATE_LAST_UPDATE=2019-04-12<br>
Geometry: Line String<br>
Feature Count: 19752<br>
Extent: (30303.378000, 306978.314000) - (277195.394000, 609413.877062)<br>
Layer SRS WKT:<br>
PROJCS["Amersfoort / RD New",<br>
    GEOGCS["Amersfoort",<br>
        DATUM["Amersfoort",<br>
            SPHEROID["Bessel 1841",6377397.155,299.1528128,<br>
                AUTHORITY["EPSG","7004"]],<br>
            TOWGS84[565.2369,50.0087,465.658,-0.406857,0.350733,<br>-1.87035,4.0812],<br>
            AUTHORITY["EPSG","6289"]],<br>
        PRIMEM["Greenwich",0,<br>
            AUTHORITY["EPSG","8901"]],<br>
        UNIT["degree",0.0174532925199433,<br>
            AUTHORITY["EPSG","9122"]],<br>
        AUTHORITY["EPSG","4289"]],<br>
    PROJECTION["Oblique_Stereographic"],<br>
    PARAMETER["latitude_of_origin",52.15616055555555],<br>
    PARAMETER["central_meridian",5.38763888888889],<br>
    PARAMETER["scale_factor",0.9999079],<br>
    PARAMETER["false_easting",155000],<br>
    PARAMETER["false_northing",463000],<br>
    UNIT["metre",1,<br>
        AUTHORITY["EPSG","9001"]],<br>
    AXIS["X",EAST],<br>
    AXIS["Y",NORTH],<br>
    AUTHORITY["EPSG","28992"]]<br>
ogc_fid: Integer64 (10.0)
gml_id: String (254.0)
namespace: String (250.0)
lokaalid: String (250.0)
brontype: String (250.0)
bronactual: Date (10.0)
bronbeschr: String (250.0)
bronnauwke: Real (24.15)
objectbegi: Date (10.0)
objecteind: Date (10.0)
tijdstipre: Date (10.0)
eindregist: Date (10.0)
tdncode: Integer64 (10.0)
visualisat: Integer64 (10.0)
mutatietyp: String (250.0)
typeinfras: String (250.0)
typespoorb: String (250.0)
fysiekvoor: String (254.0)
spoorbreed: String (250.0)
aantalspor: String (250.0)
vervoerfun: String (250.0)
elektrific: String (3.0)
hoogtenive: Integer64 (10.0)
status: String (250.0)
brugnaam: String (250.0)
tunnelnaam: String (250.0)
baanvaknaa: String (250.0)
geometrie_: String (254.0)

### Performing projection and transformations with ogr2ogr
$ ogr2ogr spoorwegen.shp -t_srs "EPSG:4326" Top10NL_Spoorwegen.shp<br>
$ ogrinfo -so spoorwegen.shp spoorwegen<br>
INFO: Open of `spoorwegen.shp'<br>
      using driver `ESRI Shapefile' successful.<br>

Layer name: spoorwegen<br>
Metadata:<br>
  DBF_DATE_LAST_UPDATE=2019-10-22<br>
Geometry: Line String<br>
Feature Count: 19752<br>
Extent: (3.592947, 50.752341) - (7.215403, 53.462471)<br>
Layer SRS WKT:<br>
GEOGCS["WGS 84",<br>
    DATUM["WGS_1984",<br>
        SPHEROID["WGS 84",6378137,298.257223563,<br>
            AUTHORITY["EPSG","7030"]],<br>
        AUTHORITY["EPSG","6326"]],<br>
    PRIMEM["Greenwich",0,<br>
        AUTHORITY["EPSG","8901"]],<br>
    UNIT["degree",0.0174532925199433,<br>
        AUTHORITY["EPSG","9122"]],<br>
    AUTHORITY["EPSG","4326"]]<br>
ogc_fid: Integer64 (10.0)
gml_id: String (254.0)
namespace: String (250.0)
lokaalid: String (250.0)
brontype: String (250.0)
bronactual: Date (10.0)
bronbeschr: String (250.0)
bronnauwke: Real (24.15)
objectbegi: Date (10.0)
objecteind: Date (10.0)
tijdstipre: Date (10.0)
eindregist: Date (10.0)
tdncode: Integer64 (10.0)
visualisat: Integer64 (10.0)
mutatietyp: String (250.0)
typeinfras: String (250.0)
typespoorb: String (250.0)
fysiekvoor: String (254.0)
spoorbreed: String (250.0)
aantalspor: String (250.0)
vervoerfun: String (250.0)
elektrific: String (3.0)
hoogtenive: Integer64 (10.0)
status: String (250.0)
brugnaam: String (250.0)
tunnelnaam: String (250.0)
baanvaknaa: String (250.0)
geometrie_: String (254.0)

### Converting Shapefiles to GeoJSON with ogr2ogr
$ ogr2ogr -f "GeoJSON" spoorwegen.json spoorwegen.shp

Warning 1: The output driver does not natively support Date type for field eindregist. Misconversion can happen. -mapFieldType can be used to control field type conversion.

Test integrity of the output Spoorwegen.json in geojson.io

I followed the same procedure for the other five shapefiles.

### Simplify Railways File
After using mapshaper, the railways-simplified.json file was still 16 MB.
In order to decrease the size further, we removed all the properties except "gml_id". 
```shell
>ogr2ogr -f "GeoJSON" -select gml_id data\railways-simplified1.json data\railways-simplified.json
```

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
