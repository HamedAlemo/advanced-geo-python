# Designing and Automating Data Workflows in Python

**Attribution**
*This lecture is designed based on great resources available on [Earth Data Science Workflows](https://www.earthdatascience.org/courses/use-data-open-source-python/earth-data-science-workflows/) from Earth Lab CU Boulder.*

Designing workflows to process and create outputs for many large files and datasets is a key skill in Earth Data Analytics. Yet it is something that most scientists and Earth analysts learn on the fly at some point in their careers. Now that you have learned various Python packages for geospatial data processing, we are going to discuss the ways you would go after designing and automating your data workflows. 

In this chapter, you will learn how to identify key steps in designing a data workflow and how to write pseudo code to outline data workflow. You will also learn the ways you can modularize your code and test it. We will use examples of geospatial data workflows to walk through different steps of designing these workflows. 

The outline below identifies several key steps associated with designing a workflow that can help you structure your thinking and develop an effective design. 

## Identify the Problem, Challenge or Question

To begin you need to clarify the question(s) or challenge(s) that you need to address. Knowing the specific problem that you need to solve will help to set bounds on what your workflow does and does not need to do.

In this chapter, we will use the example of calculating a time series of normalized difference vegetation index (NDVI) to investigate ecological processes and changes.

NDVI is usually used to study changes due to a disturbance such as a flood or a fire. But NDVI can also be used to understand seasonality - when vegetation in an area begins to “green-up” or grow once conditions allow it (after the winter cold in temperate regions, or after the rainy season begins in dry climates) and “brown down” when vegetation begins to die back.  You can calculate NDVI for each month of the year (or even for several years) to understand seasonality in a particular study area. 

Different areas in different parts of the world have different seasonal patterns. For example, the NEON <a href="https://www.neonscience.org/field-sites/field-sites-map/SJER" target="_blank">San Joaquin Experimental Range (SJER)</a> in central California has a Mediterranean climate: its grasses and oaks green up with the onset of winter rains, reach peak greenness in early spring, and brown down by late spring as the soil dries out during the hot, dry summer. In contrast, the NEON <a href="https://www.neonscience.org/field-sites/field-sites-map/HARV" target="_blank">Harvard Forest (HARV)</a> site in Massachusetts is a temperate deciduous forest that greens up in late spring (around May), stays green through the summer, and browns down in the fall.   

Because their seasonal cycles are nearly opposite, these two sites are ideal for comparisons of NDVI to identify differences in seasonality across sites and will be used as the study areas for the data workflow challenge. 

Changes in seasonality can be important indicators of ecological change. For example, if green-up begins earlier, such that fruit or seed resources become available sooner than average, animals that forage on the fruits in the spring must either migrate earlier to use these resources, or miss out on them if they do not adjust migration behavior. This phenomenon is referred to as a phenological mismatch.

## Identify the Data Needed to Address the Question or Challenge

Once you have a question in mind, it is time to figure out your data requirements. Requirements are the qualities that your data need to have in order to address a particular question well. 

For our challenge of calculating a NDVI time series, the goal is to create a time series of NDVI for a study area across a year. 

As you want to explore seasonal patterns of “green-up” and “brown down”, you need data that is at least collected each month. 

What data do you select for your analysis? Consider temporal frequency of data collection and spatial resolution. 

For example, NAIP is collected only every two to three years, and only during the leaf-on growing season, so it cannot capture seasonal changes. 

In contrast, MODIS and Landsat may be more useful. MODIS images most of the Earth every day, while each Landsat satellite revisits a location every 16 days (every 8 days with Landsat 8 and 9 combined). 

In terms of resolution, MODIS pixels (250 m for the red and near-infrared bands) could be too large depending on the size of your study site, while Landsat pixels are 30 m. Also note that the Terra and Aqua satellites that carry MODIS reach the end of their missions in 2027, and NASA recommends VIIRS products as the successor for long-term records. Perhaps Landsat has an ideal combination of temporal frequency, resolution and spatial coverage, and it is the dataset we will use in this chapter.

Denser alternatives are also worth knowing about: Sentinel-2 observes a location every 5 days at 10 m resolution, and the Harmonized Landsat Sentinel-2 (HLS) product combines both missions at 30 m to observe a location every 2 to 3 days. More frequent observations are especially helpful in cloudy places, where many scenes are unusable.


## Design Your Workflow

Next it is time to design the workflow to create the output(s) that will address your question or challenge. 

To use the NDVI time series to understand seasonality, it can be helpful to create a plot that shows the NDVI values for each month for a site.  In addition, you may want to produce some output files (e.g. CSV files) that you can share with others who may be interested in creating their own visualizations. You need to understand your users' needs to better design the requirements for your output. 

For the NDVI time series challenge, you will design a workflow that has two outputs:

1. A plot of average NDVI (for each Landsat image) for 2 sites over a year.
2. A CSV file containing the average NDVI values (for each Landsat image) for both sites. 

Once you know your outputs, you can work backwards to determine the data and steps needed to create your final output(s). 

The design process can feel difficult, so it can be helpful to begin the design of the workflow using words (not code), a process known as pseudocoding. With pseudocode, you list out the inputs and outputs of the workflows and then identify the analytical steps needed to create the outputs from the inputs.

Next lecture walks you through the pseudocoding process, so that you can use this method to easily design data workflows and move toward automating these workflows. 


## Implement Your Workflow

Once you have designed your workflow (using pseudocode first!), it is time to implement. This is where you can put all of your programming skills to the test. 

Try to write code that is clear, efficient, well documented and expressive. Remember that you never know when you may have to re-run or re-use an analysis, and you never know when someone else might need to use your code, too.

Thus, your aim should be to write code that is readable, reproducible, and efficient. Be sure to: 

1. Use clear, expressive names for objects, files, etc. Ask yourself if someone reading your code could guess what is contained in that object or file based on the name. 
2. Use reproducible paths for input data and writing outputs (e.g. use `os.path.join()` or the more modern `pathlib.Path` to define paths, include code to create needed directories, etc).   
3. Write custom functions for repetitive tasks in your workflows.
4. Include checks (i.e. tests) in your code to ensure that it is doing what you think it is! 

We reviewed some of these topics in our lectures on [Python Environments](03_python-env.md) and the assignment based on [NASA Open Science 101 module](../files/open-science-101-v-1-0-0/README.md), and more programming specific best practices are introduced in [Data Workflow Best Practices](../lectures/24_workflows_best_practices.ipynb).

```{admonition} With an AI agent
:class: note
The steps in this lecture are the part of the work you cannot hand to an AI coding agent. An agent can write code to calculate NDVI in seconds, but it does not know that NAIP is collected only in the growing season, that your users want a csv file, or that SJER and HARV should have nearly opposite seasonal cycles. Write these decisions down: the question, the data and why it fits, the exact outputs, and any constraints. This is the content of the `AGENTS.md` file from [Working with GenAI Tools](04_working_with_genai_tools.md). The agent reads it at the start of every session, which keeps it working on your problem instead of one it guessed. You will write one for this workflow in the [lab](25_agentic_workflow_lab.md).
```

<p>&nbsp;</p>