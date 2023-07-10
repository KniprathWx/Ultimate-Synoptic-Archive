"""
Ultimate Synoptic Archive VERSION 3.00
Released: 07/10/2023

Version 3.00 Changelog:
    -New Features:
        -New Map Type --> Synoptic Composite (inspired by Tomer Burg's Synoptic Composite Map)
            -Includes 250mb winds, 500mb vort/heights, 850mb winds, MSLP, and PWAT
        -New Map Type --> Severe Weather Threat Index
            -Read more about the index here: https://github.com/Unidata/MetPy/issues/634
        -CAPE Map was *removed* with this update due to missing data points (2011-2020) in the GFS Archive
            -A potential fix to this could be computing CAPE
                -Currently not aware of any way to do this over a 2d grid (effectively)
        -New Map Type --> Apparent Temperature
            -Map only includes surface apparent temperature
        -All maps now feature a black background with white titles (fixes odd black border problem)
        -Removed option for mph or knots, now all maps are locked in knots (synoptic composite is m/s)
            -Mph, kmh, and m/s options will be added in a future version
            -However, additional stylistic/colormap changes are needed, and this is a low priority at this time
    -Other Minor Changes:
        -Added a few lines of code for plotting High/Low Pressure on sectors outside of CONUS
        -Changed name of "SurfaceMap" to "SurfaceTempsMap" to make room for other surface map types
        -Added highs/lows plotting to 850mb Theta-E Map
        -Added 'extend' kwarg to contourf certain plots to handle exceedance of set max/min values
            -Some issues still with exceedance values and further work is needed
        -Added handling to check if requested data file already exists before initiating download
        -Added improved handling for sector and windslice selection (eliminates repetitive code)
        -Slight stylistic changes were made to the end-of-code map creation sequence handling
        -Titles to maps were revamped to look more stylistically appealing
            -Valid time now appears in the right title slot
            -Main title was bolded and font sizes were changed
            -'Created by' title added (with new code for in map text to fix previous issues)
    -Bug Fixes:
        -Fixed data download code (again)
        -Got rid of those pesky code depreciation warnings

___________________________________________________________________________________________________________________

*IMPORTANT* steps to using this code successfully:
    1: Be sure to enter *ALL* required information in code cell 3 below
        ---> This includes the save location... You may need to create a new folder where this notebook is located
    2: *AFTER* you have entered all of the correct information, run *ALL* cells
    3: Wait at the last code cell for prompts on successful (or unsuccessful) map creation
    4: After prompted that the map(s) have been created, check your save folder to make sure they are there

___________________________________________________________________________________________________________________

Troubleshooting checklist:
    1: The code ran successfully, but my maps have no or incorrect data plotted on them
        -Try re-running the code
        -If the issue persists, try running a different case date (I recommend 12/28/2021 as I know it works)
        -If changing the case date solves the issue, your case date's data may be corrupted
    2: I am getting an error during "URL Fetching":
        -Is your case date between January 1, 1979 and a month ago? If not, data is not available for your case
            -If yes, then make sure your date is correctly input into code cell 3 (ie: leading zero for month/day 1-9)
        -If the issue persists, try running a different case date (I recommend 12/28/2021 as I know it works)
            -If changing the case date solves the issue, your case date's data may be missing
    3: I am getting an error thrown on the "plt.savefig" line
        -Make sure your save location in code cell 3 exists (ie: you have created a folder and inserted the name in cell 3)  

___________________________________________________________________________________________________________________

Known Issues:
    -Missing data at the Prime Meridian (Affects Europe projection *ONLY*)
        -Some solutions to this problem exist online, but are not immediately compatible with PyGrib Grids
    -925mb frontogenesis may struggle to plot for certain cases ---> Unknown cause at this time
    -Date/time text (upper right of map) randomly changes size ----> Unknown cause at this time

___________________________________________________________________________________________________________________

Future Plans:
    -Add handling for multiple timestep input
    -Add further handling for max/min exceedance
    -Further development of 925 Frontogensis Map
        -More of a layer average approach will be favored in future versions
    -More map types are still being developed (these may not occur depending on coding/data limitations)
        -Precip-Type Map
        -SFC/MU/ML CAPE Maps
        -500-750mb Lapse Rates Map
    -Add more sector view options
        -Currently planned additions: Canada, Atlantic, and China
    -Separate upcoming projects:
        -ERA5 dataset implementation with the below maps
        -Southern Hemisphere version of these maps
        -Ultimate Mesoscale Archive (HRRR/RAP data and more maps!)

___________________________________________________________________________________________________________________

If you: 
    -Find any bugs while using the code (not already outlined in "known issues" above)
    -Are having problems with the code (and have went through the troubleshooting checklist above)
    -Have suggestions for new features/map types to be added to the code
---> Please let me know! Twitter is probably the best way to contact me: @KniprathWx

"""
