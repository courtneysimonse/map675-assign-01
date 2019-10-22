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
* $ gdalinfo --version
GDAL 2.4.1, released 2019/03/15

* $ ogrinfo -so Top10NL_Spoorwegen.shp Top10NL_Spoorwegen

INFO: Open of `Top10NL_Spoorwegen.shp'
      using driver `ESRI Shapefile' successful.

Layer name: Top10NL_Spoorwegen
Metadata:
  DBF_DATE_LAST_UPDATE=2019-04-12
Geometry: Line String
Feature Count: 19752
Extent: (30303.378000, 306978.314000) - (277195.394000, 609413.877062)
Layer SRS WKT:
PROJCS["Amersfoort / RD New",
    GEOGCS["Amersfoort",
        DATUM["Amersfoort",
            SPHEROID["Bessel 1841",6377397.155,299.1528128,
                AUTHORITY["EPSG","7004"]],
            TOWGS84[565.2369,50.0087,465.658,-0.406857,0.350733,-1.87035,4.0812],
            AUTHORITY["EPSG","6289"]],
        PRIMEM["Greenwich",0,
            AUTHORITY["EPSG","8901"]],
        UNIT["degree",0.0174532925199433,
            AUTHORITY["EPSG","9122"]],
        AUTHORITY["EPSG","4289"]],
    PROJECTION["Oblique_Stereographic"],
    PARAMETER["latitude_of_origin",52.15616055555555],
    PARAMETER["central_meridian",5.38763888888889],
    PARAMETER["scale_factor",0.9999079],
    PARAMETER["false_easting",155000],
    PARAMETER["false_northing",463000],
    UNIT["metre",1,
        AUTHORITY["EPSG","9001"]],
    AXIS["X",EAST],
    AXIS["Y",NORTH],
    AUTHORITY["EPSG","28992"]]
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
$ ogr2ogr spoorwegen.shp -t_srs "EPSG:4326" Top10NL_Spoorwegen.shp
$ ogrinfo -so spoorwegen.shp spoorwegen
INFO: Open of `spoorwegen.shp'
      using driver `ESRI Shapefile' successful.

Layer name: spoorwegen
Metadata:
  DBF_DATE_LAST_UPDATE=2019-10-22
Geometry: Line String
Feature Count: 19752
Extent: (3.592947, 50.752341) - (7.215403, 53.462471)
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
