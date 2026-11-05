# Learn to Write Pseudocode for Python Programming
**Attribution** 
*This lecture is designed based on great resources available on [Earth Data Science Workflows](https://www.earthdatascience.org/courses/use-data-open-source-python/earth-data-science-workflows/) from Earth Lab CU Boulder.*

Pseudocode can help you design data workflows through listing out the individual steps of a workflow in plain language, so the focus is on the overall data process, rather than on the specific code needed. 


## Design an Efficient Data Workflow Using Pseudocode

You have now identified your challenge - to calculate and plot average normalized difference vegetation index (NDVI) for every Landsat scene (individually) across one year for two study locations:

1. <a href="https://www.neonscience.org/field-sites/field-sites-map/SJER" target="_blank">San Joaquin Experimental Range (SJER) in central California, United States</a>
2. <a href="https://www.neonscience.org/field-sites/field-sites-map/HARV" target="_blank">Harvard Forest (HARV) in Massachusetts, United States</a> 

You have been given a study area boundary for each site. Your next step is to write out the steps that you need to follow to get to your end goal plot and csv file. 

You know you will need to do the following:

1. Find Landsat scenes.
2. Access the scenes on the cloud or download them.
3. Read the data.
4. Calculate NDVI.
5. Save NDVI values to pandas dataframe with the associated date and site name
6. Export NDVI values to a csv file
7. Plot NDVI time-series

Begin your process by pseudocoding - or writing out steps in plain English - everything that you will need to do in order to get to your end goal. The steps below will walk you through beginning this process of writing pseudocode.

For each block of pseudocode, also write down its inputs (what the steps need) and outputs (what the steps produce). This makes the flow of data through your workflow explicit, and a block with clear inputs and outputs is a natural candidate for a function, which you will learn about in the next lesson.


## Begin With the Workflow for One Landsat Scene

1. Search for one Landsat scene across your area of interest (aoi)

2. Get a list of relevant files for the resulting Landsat scene.

    Recall that Landsat data is provided as a series of Cloud-Optimized GeoTIFF (COG) files - one for each band (e.g. red, near-infrared) and one with the pixel quality assurance information (`QA_PIXEL`), which flags clouds and cloud shadows. 

    ```{admonition} Steps required to get data for one Landsat scene for a site
    1. Query an API to find the target Landsat scene
    2. Get a list of files/assets for that scene.
    3. Subset the list to just the files/assets required to calculate NDVI.
    ```

3. Open and crop the data for one Landsat scene. 

    Now that you have the steps to get the data for one Landsat scene, you can expand your pseudocode steps to include opening and cropping the data to the site boundary. 

    ```{admonition} Steps required to process one Landsat scene for a site
    1. Query an API to find the target Landsat scene
    2. Get a list of files/assets for that scene.
    3. Subset the list to just the files/assets required to calculate NDVI.
    4. Open and crop the bands needed to calculate NDVI.
    ```

4. Calculate NDVI for one Landsat scene. 

    Last, you can expand your pseudocode to include using the bands that you opened and cropped to calculate NDVI. 

    ```{admonition} Steps required to process one Landsat scene for a site
    Inputs: the site boundary (aoi) and the date (or date range) to search.

    Outputs: the average NDVI value and the acquisition date for that scene.

    1. Query an API to find the target Landsat scene
    2. Get a list of files/assets for that scene.
    3. Subset the list to just the files/assets required to calculate NDVI.
    4. Open and crop the bands needed to calculate NDVI.
    5. Calculate average NDVI for that scene.
    ```

## Expand Workflow to Include All Landsat Scenes for a Site

You have now identified the steps required to process a single Landsat scene. Those steps now need to be repeated across all of the scenes for each site for a year. 

```{admonition} Steps required to process all Landsat scenes for a site 
1. Query an API to find all Landsat scenes for your aoi
2. For each scene, use the steps outlined previously for one scene to calculate NDVI for the data in that scene.
3. Save NDVI value and date for that scene (there are some steps here that you need to flesh out as well) to a list or dataframe that contains average NDVI for each scene at this site.

```

OK - now you are ready to put the workflow for a single site together. Of course, remember there are some sub steps that have not been fleshed out just yet, but start with the basics and build from there.


```{admonition} Steps required to process all Landsat scenes for a site
Inputs: the site name, the site boundary (aoi) and the date range to search (e.g. one year).

Outputs: a csv file with the date and average NDVI of each scene at the site, and a plot of the NDVI time series for the site.

1. Query an API to find all Landsat scenes for your site
2. For each scene, use the steps outlined previously for one scene to calculate NDVI:
    - Get a list of files/assets for that scene.
    - Subset the list to just the files/assets required to calculate NDVI.
    - Open and crop the bands needed to calculate NDVI.
    - Calculate average NDVI for that scene.
3. Save NDVI values and the date for that scene (there are some steps here that you need to flesh out as well) to a list or dataframe that contains average NDVI for each scene at this site.
4. Export dataframe with mean NDVI values to csv. (i.e. a “data product” output that you can share with others)
5. Plot the NDVI for each Landsat scene
```

## Add Multiple Sites Worth of Data to Your Workflow

In the previous section, you began to think about the steps associated with creating a workflow for:
1. A single Landsat scene. 
2. A set of Landsat scenes for a particular site.

But you want to do this for two or more sites so you need to design a workflow that allows for two or more sites as input. Add an additional layer to your pseudo code:

```{admonition} Modular workflow for many sites
Inputs: a list of sites (each with a name and a boundary) and the date range to search.

Outputs: a single csv file (e.g. `all-sites-ndvi.csv`) with the site name, date and average NDVI of each scene, and one plot showing the NDVI time series of all sites.

- Get a list of all the sites.
- For each site:
    1. Query an API to find all Landsat scenes for that site
    2. For each scene, use the steps outlined previously for one scene to calculate NDVI for the data in that scene:
        - Get a list of files/assets for that scene.
        - Subset the list to just the files/assets required to calculate NDVI.
        - Open and crop the bands needed to calculate NDVI.
        - Calculate average NDVI for that scene.
    3. Save the NDVI value, date and site name for each scene (there are some steps here that you need to flesh out as well) to a list or dataframe that contains average NDVI for each scene at this site.
- Combine the results from all sites into one dataframe.
- Export the combined dataframe with mean NDVI values to a single csv file (i.e. a “data product” output that you can share with others).
- Plot the NDVI time series for all sites on one plot.
```

Notice that exporting the csv file and plotting now happen after the loop over sites, not inside it. The goal is one csv file and one plot that include both sites, so you first need to collect the results from every site and combine them. If these steps stayed inside the loop, you would end up with a separate csv file and a separate plot for each site.

You have now designed a workflow using pseudocode to process several sites worth of Landsat data. 

Of course, the pseudocode above is just beginning. For each of the steps above, you need to flesh out how you can accomplish each task. 

```{admonition} Exercise: What is missing from this pseudocode?
:class: tip
Look again at the steps for processing one Landsat scene. They would run, but they would not produce NDVI values you can trust. Before opening the answer below, list the steps you think are missing.
```

```{admonition} Answer
:class: dropdown
- Filter the search results by the cloud cover reported in each scene's metadata, so that you skip mostly cloudy scenes before reading any data.
- Reproject the site boundary to the CRS of the scene before cropping. Landsat scenes are stored in UTM projections, while site boundaries are often in latitude/longitude.
- Mask clouds and cloud shadows using the `QA_PIXEL` band. Even a few cloudy pixels inside the site can pull the average NDVI down.
- Apply the scale factor and offset for Landsat Collection 2 Level-2 surface reflectance before calculating NDVI. The raw band values are stored as integers and are not reflectance values, and because of the offset, NDVI calculated from the raw values is wrong.
- Skip scenes where too few clear pixels remain inside the site after masking (for example, less than half of the site).
- Handle dates with more than one scene. This happens when a site falls in the overlap between two neighboring scenes along the same orbit path, so you need to decide whether to merge them or keep only one.
```

The next lesson in this chapter focuses on data workflow best practices that can help you implement your workflow efficiently and effectively. 

```{admonition} With an AI agent
:class: note
Pseudocode is the plan you give a coding agent, and the habits from this lecture carry over directly. Build in steps: ask the agent for the one-scene workflow, check and commit it, then expand to one site and then to many sites, each in a new session. Small steps are easier to review and use fewer credits. The inputs and outputs of each block are the interfaces you want the agent to implement, so state them explicitly. Also expect the agent to fill gaps in your pseudocode without telling you, sometimes correctly and sometimes not. Before it writes any code, you can ask it to critique your plan and compare its answer with the exercise above. You will do both in the [lab](25_agentic_workflow_lab.md).
```

<p>&nbsp;</p>