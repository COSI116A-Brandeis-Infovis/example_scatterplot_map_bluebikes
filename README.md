# Example Programming: Blue Bikes
In this activity, you are going to create a spatial visualization the easy way.  More specifically, we have built a scatterplot with a map background, so that the points that are overlaid have spatial significance.

This is one strategy you can use to build a map with interactivity for your final project.  Note that the provenance of the map image, found in `boston.png`, has been lost to time.  You can use open source map data or a free account on an open source platform like <a href="https://maphub.net/" target="_blank">Map Hub</a>  or <a href="http://bboxfinder.com" target="_blank">bboxfinder</a> to get a screenshot to use as the background of your map.

## Data

We will be visualizing publicly available data from BlueBikes, the bike share program around the Boston area.  To prepare for this assignment, we downloaded [publicly available data from BlueBikes](https://www.bluebikes.com/system-data), including all bike rentals in the month of March, 2017.  We then grouped by the station names, and got counts of the incoming and outgoing rentals at each location.  If you are curious, you can see our data wrangling script in the `/data/` folder, in a [jupyter notebook](https://jupyter.org/).


## Adding the map background

In this example, we started with a plain scatterplot on the page.  If you look into the code, you'll see that we're parsing the `data/march2017_bluebikes_trip_counts.csv` file, and mapping the `latitude` and `longitude` to the `x` and `y` axes respectively.

First, we needed to determine what the bounding box of our map area should be.  Looking into `spatial.js`, you'll see that we output the minimum and maximum latitudes and longitudes into the console:

    console.log("minX is ", minX);
    console.log("minY is ", minY);
    console.log("maxX is ", maxX);
    console.log("maxY is ", maxY);

In your browser, open the javascript console and look at what the corresponding values are for the bounding box coordinates.  Then, go to the site [bboxfinder.com](bboxfinder.com), and enter your bounding box coordinates.  First, click on the bounding box selector on the left side of the page.

![Click on left side](bboxfinder1.png)

Then, paste your bounding box coordinates in the form (minX, minY, maxX, maxY), and click "Add".

![Enter on the right side](bboxfinder2.png)

You will be brought to a rectangular bounding box highlighted in blue.  Take a cropped screenshot of that box ([instructions for Windows 10](https://support.microsoft.com/en-us/help/4027213/windows-10-open-snipping-tool-and-take-a-screenshot), [instructions for OS X](https://support.apple.com/en-us/HT201361)).  Save that image into the root folder of this assignment, and pass the filename into the background image field in `visualization.js`.

    let spatialPlot = spatial({
        'backgroundImage': 'my-awesome-image.png'
      })

Lastly, you need to resize your SVG so that it has the same dimensions as your screenshot.  Determine the size of your screenshot by right clicking on your image, going to properties, and finding the width and height of the image in pixels.  Then, change the width and height in `spatial.js` to those dimensions.  

## Visualizing activity per station

Now that we have a scatterplot built on top of a map, we can use an additional visual channel to communicate another attribute.  We're going to map the radius of each point to correspond to the number of trips started at that location.

In `spatial.js`, note that there's a scale used for the radius around line 85, along with the scales for the x and y axes.  Note that the choice for the radius scale is not great - some of the radii are way too large, and cause occlusion.  Change the definition of the radius scale around line 90 to make the scale return more reasonable radii.  Which aspect of the scale is responsible: the domain or the range?

