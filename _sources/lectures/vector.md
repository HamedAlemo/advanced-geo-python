# Review of Geospatial Vector Data

In this lecture, we will review geospatial vector data structures. 


**Attribution**
*The content of this lecture are modified from three excellent sources: [Introduction to Spatial Vector Data File Formats in Open Source Python](https://www.earthdatascience.org/courses/intro-to-earth-data-science/file-formats/use-spatial-data/use-vector-data/) from Earth Lab CU Boulder; [Introduction to Vector Data](https://carpentries-incubator.github.io/geospatial-python/02-intro-vector-data.html) from Software Carpentry; and [Overview of GeoJSON](https://tyson-swetnam.github.io/agic-2022/geojson/) from Cloud Native Data Workshop.*

---
## Geospatial Vector Data

Vector data structures represent specific features on the Earth’s surface, and assign attributes to those features. Vectors are composed of discrete geometric locations (x, y values) known as vertices that define the shape of the spatial object. The organization of the vertices determines the type of vector that we are working with: point, line or polygon.

- **Point**: Each point is defined by a single x, y coordinate and has a dimension of 0. Examples of point data include: sampling locations, the location of individual trees, or the location of survey plots.

- **LineString**: LineString is composed of many (at least 2) points that are connected and has a dimension of 1. For instance, a road or a stream may be represented by a line. This line is composed of a series of segments, each “bend” in the road or stream represents a vertex that has a defined x, y location.

- **Polygon**: A polygon consists of 3 or more vertices that are connected and closed and has a dimension of 2. The outlines of survey plot boundaries, lakes, oceans, and states or countries are often represented by polygons.


```{figure} ../lectures/figures/vectors.png
---
name: vectors
width: 500px
align: center
---
Types of vector objects (Source: National Ecological Observatory Network ([NEON](https://www.neonscience.org/resources/learning-hub/tutorials/intro-vector-data-r#toggle-0)))
```

If we have more than one vector data shape, you can create a `multiple` type. There three of these data:

- **MultiPoint**: A `MultiPoint` geometry is represented by multiple coordinate point pairs

- **MultiLineString**:

- **MultiPolygon**:


## GeoJSON Schemas

In this class, we will mostly use GeoJSONs for vector data formats (refer to the lecture on [The Landscape of Geospatial Data and Tools](../lectures/landscape.md) for more information about different formats.) You can represent any vector data type in GeoJSON format as described in the schemas in the following. Based on the latest [GeoJSON specification](https://datatracker.ietf.org/doc/html/rfc7946), all coordinates should be recorded using a geographic coordinate reference system, using the World Geodetic System 1984 (WGS 84) [WGS84] datum, with longitude and latitude units of decimal degrees. 

```{dropdown} GeoJSON Point Schema
``` json
{ 
  "type": "Point",
  "coordinates": [-112.4471, 34.5510]
}
```


```{dropdown} GeoJSON LineString Schema
``` json
{
  "type": "LineString",
  "coordinates": [ 
      [-112.4470, 34.5510], [-112.4695,  34.541]  
    ]
}
```

```{dropdown} GeoJSON Polygon Schema
``` json
{
  "type": "Polygon",
  "coordinates": [
      [[-112.485, 34.529], [-112.445, 34.529], [-112.445, 34.559], [-112.485, 34.559], [-112.485, 34.529]]
    ]
}
```

```{dropdown}  GeoJSON MultiPoint Schema
``` json
{
  "type": "MultiPoint",
  "coordinates": [
      [-112.4470, 34.5510],
      [-112.4695,  34.541] 
    ]
}
```

```{dropdown} GeoJSON MultiLineString Schema
``` json
{
  "type": "MultiLineString",
  "coordinates": [
      [[-112.44708, 34.5510], [-112.46953, 34.540924]], 
      [[-112.4471, 34.5510], [-112.4541,34.54447], [-112.46953, 34.540924]]
    ]    
}
```

```{dropdown} GeoJSON MultiPolygon Schema
``` json
{
  "type": "MultiPolygon",
  "coordinates": [
    [
      [[-112.0, 35.0], [-112.0, 34.0],  [-113.0, 34.0],  [-113.0, 35.0],  [-112.0, 35.0]]
    ],
    [
      [[-112.50, 35.50], [-112.50, 34.50], [-113.50, 34.50],  [-113.50, 35.50], [-112.50, 35.50]]
    ],
    [
      [[-111.50, 34.50], [-111.50, 33.50], [-112.50, 33.50],  [-112.50, 34.50], [-111.50, 34.50]]
    ]
  ]
}
```

```{dropdown} GeoJSON GeometryCollection
``` json
{
  "type": "GeometryCollection",
  "geometries": [{
      "type": "Point",
      "coordinates": [-112.4471, 34.5510]
  }, {
      "type": "LineString",
      "coordinates": [
          [-112.4470, 34.5510], [-112.4695,  34.541]  
        ]
  }]
}
```

```{dropdown} GeoJSON Feature
``` json
{
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [-112.4470, 34.5510]
  },
  "properties": {
    "name": "AGIC Venue"
  }
}
```

```{dropdown} GeoJSON FeatureCollection Point
``` json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "Location Name" : "Prescott Resort and Conference Center"
      },
      "geometry": {
        "type": "Point",
        "coordinates": [
          -112.44677424430846,
          34.55109119815299
        ]
      }
    }
  ]
}
```

```{dropdown} GeoJSON FeatureCollection with multiple attributes
``` json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "LineString",
        "coordinates": [
          [
            -112.44717121124268,
            34.551069106918945
          ],
          [
            -112.45414495468138,
            34.54447682068866
          ],
          [
            -112.46953010559082,
            34.540924192549795
          ]
        ]
      }
    },
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "Point",
        "coordinates": [
          -112.44691371917723,
          34.551210490715455
        ]
      }
    }
  ]
}
```

## Properties

Vector data has some important advantages:

- The geometry itself contains information about what the dataset creator thought was important
- The geometry structures hold information in themselves - why choose point over polygon, for instance?
- Each geometry feature can carry multiple attributes instead of just one, e.g. a database of cities can have attributes for name, country, population, etc
- Data storage can be very efficient compared to rasters

The downsides of vector data include:

- Potential loss of detail compared to raster
- Potential bias in datasets - what didn’t get recorded?
- Calculations involving multiple vector layers need to do math on the geometry as well as the attributes, so can be slow compared to raster math.


## Tools to Inspect and Manipulate GeoJSON Data

JSON is a lightweight, text-based, language-independent data interchange format. As a result, you can create and edit GeoJSON files in any text editor software. 

You can open these files in VS Code. There are multiple extensions in VS Code (such as *Geo Data Viewer*) which you can use to visualize GeoJSON in VS Code. You can certainly open then in QGIS as well. 

In the next lecture, you will learn how to work with geospatial vector data in Python. 


<p>&nbsp;</p>