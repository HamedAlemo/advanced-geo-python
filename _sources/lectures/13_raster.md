# Review of Raster Data

In this lecture, we will review geospatial raster data structures. 


**Attribution**
*The content of this lecture are modified from two excellent sources: [Introduction to Raster Data in Python](https://www.earthdatascience.org/courses/intro-to-earth-data-science/file-formats/use-spatial-data/use-vector-data/) from Earth Lab CU Boulder; and [Introduction to Raster Data](https://carpentries-incubator.github.io/geospatial-python/02-intro-vector-data.html) from Software Carpentry.*

---
## Geospatial Raster Data

Raster data are a primary type of data for geospatial assets. Rasters are stored as a grid of values which are rendered on a map as pixels. Each pixel value represents an area on the Earth’s surface. 

## What is a Raster?

Raster data is any pixelated (or gridded) data where each pixel is associated with a specific geographic location. The value of a pixel can be continuous (e.g. elevation) or categorical (e.g. land use). If this sounds familiar, it is because this data structure is very common: it’s how we represent any digital image. A geospatial raster is only different from a digital photo in that it is accompanied by spatial information that connects the data to a particular location. This includes the raster’s extent and cell size, the number of rows and columns, and its coordinate reference system (or CRS).

```{figure} ../lectures/figures/rasters.png
---
name: rasters
width: 600px
align: center
---
Raster data concept (Source: National Ecological Observatory Network ([NEON](https://www.neonscience.org/resources/learning-hub/tutorials/introduction-working-raster-data-r#toggle-0)))
```

Some examples of continuous rasters include:

- Precipitation maps.
- Maps of tree height derived from LiDAR data.
- Elevation values for a region.

Some rasters contain categorical data where each pixel represents a discrete class such as a land cover type (e.g., “forest” or “grassland”) rather than a continuous value such as elevation or temperature. Some examples of classified maps include:

- Land cover / land use maps.
- Tree height maps classified as short, medium, and tall trees.
- Elevation maps classified as low, medium, and high elevation.

## Resolution

A resolution of a raster represents the area on the ground that each pixel of the raster covers. So, a 1 meter resolution raster, means that each pixel represents a 1 m by 1 m area on the ground. The image below illustrates the effect of changes in resolution.

```{figure} ../lectures/figures/raster_resolution.png
---
name: raster_resolution
width: 600px
align: center
---
Rasters can be stored at different resolutions. The resolution simply represents the size of each pixel cell. (Source: National Ecological Observatory Network ([NEON](https://www.neonscience.org/resources/learning-hub/tutorials/introduction-working-raster-data-r#toggle-0)))
```

## Raster Bands

A raster can contain one or more bands. One type of multi-band raster dataset that is familiar to many of us is a color image. A basic color image consists of three bands: red, green, and blue. Each band represents light reflected from the red, green or blue portions of the electromagnetic spectrum. The pixel brightness for each band, when composited, creates the colors that we see in an image.

Another type of multi-band raster data is time series in which observations of the same variable (single band) over the same area are stacked together. 

We can plot each band of a multi-band image individually. Or we can composite all three bands together to make a color image. In a multi-band dataset, the rasters will always have the same extent, resolution, and CRS.

## NoData Values in Rasters
Raster data often has a `NoDataValue` associated with it. This is a value assigned to pixels where data are missing or no data were collected.

By default the shape of a raster is always square or rectangular. So if we have a dataset that has a shape that isn't square or rectangular, some pixels at the edge of the raster will have `NoDataValues`. This often happens when the data were collected by an airplane or satellite which only flew over some part of a defined region.
