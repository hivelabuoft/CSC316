<!---
layout: labold
exclude: true
--->

# Lab 6 Handout
## Introduction
### Pre-Reading Quiz
Please fill out the pre-reading quiz on Quercus *before* the beginning of class!

### Learning Objectives

- Understand the concept of D3 layouts and be able to use D3 layouts for advanced visualizations
- Know how to work with the GeoJSON and TopoJSON file format
- Have a basic understanding of geographical projections
- Know how to load multiple files sequential and parallel
- Know how to convert geodata to screen coordinates with D3 in order to create interactive maps


### Prerequisites

- You have read and **programmed** along with chapter 13, and 14 (p. 281-295) in *D3 - Interactive Data Visualization for the Web*.
- Optional reading: p. 295-322 in *D3 - Interactive Data Visualization for the Web*.

### Summary

In this lab, you will learn how to use D3 layout methods to implement more complex svg shape elements (in contrast to rect or circle elements).
After drawing an interactive pie-chart as a warm-up, the main task of the lab will be to create an interactive choropleth map.

### Useful links for this week's lab

- Comprehensive overview for [SVG Elements and Attributes](https://oreillymedia.github.io/Using_SVG/guide/markup.html)
- https://github.com/d3/d3-geo


----



## D3 Shapes

> The D3 shape methods have no direct visual output. Rather, D3 shapes take data that you provide and re-map or otherwise transform it, thereby generating new data that is more convenient for a specific task. (Scott Murray)

Visualizations typically consist of discrete graphical marks, such as symbols, arcs, lines and areas. While the rectangles
of a bar chart may be easy enough to generate directly using SVG or Canvas, other shapes are complex, such as rounded annular
sectors and centripetal Catmull–Rom splines. The D3 shape module provides a variety of shape generators for your convenience.

![D3 Shapes](assets/cs171-d3-layouts.png?raw=true "D3 Shapes")

Each shape may have distinct features not shared by others, so make sure to consult the D3 documentation([https://github.com/d3/d3-shape/blob/master/README.md](https://github.com/d3/d3-shape/blob/master/README.md)) for implementation details. You will learn more about a few selected shapes in this lab.

&nbsp;

### Pie Shape

In this week's lab, we will introduce you to D3 shapes by creating a simple pie chart. We will
 make use of the pie shape generator, i.e. the ***d3.pie()*** method, which computes
  the start and end angles of arcs that comprise a pie or donut chart.

*Example:*

```javascript
// Initialize data
let data = [45,30,10];

// Define a default pie layout
let pie = d3.pie();

// Call the pie function
pie(data);
```

*Console Output:*

![D3 Pie Shape Generator](assets/cs171-d3-pie-console-output.png?raw=true "D3 Pie Shape Generator")

The D3 pie shape takes a dataset and creates an array of objects. Each of those objects contains
 a value from the original dataset, along with additional data, like *startAngle* and *endAngle*.
 That's all there is to the D3 pie shape. It has no visual output, but transforms the input
  data in a way that it is much more convenient for drawing a pie chart.

&nbsp;

Now that we understood how the pie generator works, let's draw the actual pie chart. We'll use an
 arc generator ***d3.arc()*** to generate the paths for the pie segments. Take a few minutes to
  look through the following code example:

```javascript

// SVG drawing area
let width = 300,
    height = 300;

// Position the pie chart (currently only a placeholder) in the middle of the SVG area
let svg = d3.select("body").append("svg")
    .attr("width", width)
    .attr("height", height)
    .append("g")

// pie chart setup
let pieChartGroup = svg
    .append('g')
    .attr('class', 'pie-chart')
    .attr("transform", "translate(" + width / 2 + "," + height / 2 + ")");

// Initialize the data
let data = [45,30,10];

// Define a default pie layout
let pie = d3.pie();

// Ordinal color scale (10 default colors)
let color = d3.scaleOrdinal(d3.schemeCategory10);

// Pie chart settings
let outerRadius = width / 2;
let innerRadius = 0;      // Relevant for donut charts

// Path generator for the pie segments
let arc = d3.arc()
    .innerRadius(innerRadius)
    .outerRadius(outerRadius);

// Bind data
let arcs = pieChartGroup.selectAll(".arc")
    .data(pie(data))

// Append paths
arcs.enter()
    .append("path")
    .attr("d", arc)
    .style("fill", function(d, index) { return color(index); });
```


> **Important Notice**
>
> We have used a pie chart as an example because it is one of the most popular chart types, and
> it demonstrates the concept of D3 shapes very well. However, it is also very important to
> mention that pie charts are often not the best way to represent data! Humans are not very good
> at comparing slices of a circle, and pie charts easily lead to misunderstandings or give false
> impressions of the data. Usually, other visualization methods are more effective, so most of
> the time you shouldn't use pie charts. If you do, make sure to compare only a very low number
> of elements within these charts.

&nbsp;


## Geomapping

In the second part of this lab we will focus on a different topic: We want to show you how to convert geographical data to screen coordinates, in order to create interactive maps. These maps can show specific regions, countries or whole continents. You will learn how to render geographic data as paths, how to assign colors and how to draw data points on top of the map.


### GeoJSON

GeoJSON is a JSON-based standard for encoding a variety of geographic data structures. We need the data (e.g., country boundaries, points of interests) in a proper format to generate visualizations of geographic data. Web browsers and especially D3 are not able to render traditional shapefiles, which are used by experts in geographic information systems (GIS). Therefore, GeoJSON has been established as a common way to store this information for use in web browsers.

The sub-units in GeoJSON files are called ***Features***. They contain the geodata (points, polygons, lines, ...) and very often additional information about the objects, for example, the names and the ISO codes of countries. All the features are part of the main object, the ***FeatureCollection***.

*Example:*

```javascript
{
	"type" : "FeatureCollection",
	"features" : [
		{
		  "type": "Feature",
		  "geometry": {
		    "type": "Point",
		    "coordinates": [51.507351, -0.127758]
		  },
		  "properties": {
		    "name": "London"
		  }
		},
		{
			...
		}
	]
}
```

In this example we have a feature which represents a single geographical point. The coordinates of the point are specified as an array with longitude and latitude values (```[-0.127758, 51.507351]```). In GeoJSON the first element indicates the longitude, the second element the latitude value.

In many more cases, GeoJSON files contain complex polygon data that represent the boundaries of multiple regions or countries instead of a plain list of points:

```javascript
"geometry": {
	"type": "MultiPolygon",
	"coordinates": [[[[-131.602021,55.117982],
		[-131.569159,55.28229],[-131.355558,55.183705],
		[-131.38842,55.01392],[-131.645836,55.035827], ...
    ]]]
}
```

Depending on the resolution of the dataset, each feature will include more or less longitude/latitude pairs. As you can imagine, the size of a GeoJSON file becomes tremendously high if you store the boundaries of a whole continent in high resolution.


### TopoJSON

TopoJSON is an extension of GeoJSON that encodes topology. The generated geographical data is substantially more compact than GeoJSON and results in a file size reduction of roughly 80%.

Depending on your needs, you will probably find appropriate TopoJSON files online. You can also generate custom TopoJSON files from various formats with the TopoJSON command-line tool.

→ ***Whenever you want to use a TopoJSON file in D3, you will need the TopoJSON JavaScript library to convert the data to GeoJSON for display in a web browser:*** [http://d3js.org/topojson.v1.min.js](http://d3js.org/topojson.v1.min.js)

In addition to the GeoJSON conversion, the JS library provides further methods, for example, to get the neighbors of objects or to combine multiple regions (*topojson.mesh()*).

### Workflow to implement a map with D3

***Create projection ⇒ Create D3 geo path ⇒ Map TopoJSON data to the screen***

#### D3 projections

Drawing a geographical map in D3 requires the mapping of geographical coordinates (longitude, latitude) to screen coordinates (x, y). The functions to process the mapping are called projection methods. D3 already includes a set of the most common geo projections.

*This image shows four different projections in D3:*

![D3 Projections](assets/cs171-d3-projections.png?raw=true "D3 Projections")

*(You can take a look at the [documentation](https://github.com/d3/d3-geo/blob/master/README.md) to see more examples of geo projections.)*

When projecting positions from a sphere (i.e., the world) to a 2D plane, these different projection methods can have very different results. Different projection methods have different characteristics (e.g., distance, direction, shape, area) and show different levels of distortion.


#### D3 geo path

The path generator takes the projected 2D geometry from the last step and formats it appropriately for SVG. Or in other words, the generator maps the GeoJSON coordinates to SVG paths by using the projection function.

```javascript
let path = d3.geoPath()
    .projection(projection);
```


#### Map TopoJSON data to geo path elements

After defining the SVG area, the projection and the path generator, we can load the TopoJSON
 data, convert it to GeoJSON and finally map it to SVG paths. Here's a one-liner converting
  TopoJSON data for the US to GeoJSON. The data structure you end up with will allow you to draw a
   path for each state in the US.

```javascript
// Convert TopoJSON to GeoJSON (target object = 'states')
let usa = topojson.feature(data, data.objects.states).features
```
---

### Resource

- Chapters 13 (p. 267-289) and 14 (p. 291-325) in *D3 - Interactive Data Visualization for the Web* by Scott Murray
- [http://bost.ocks.org/mike/map/](http://bost.ocks.org/mike/map/)
- [https://github.com/d3/d3-geo/blob/master/README.mdd](https://github.com/d3/d3-geo/blob/master/README.md)
- [https://github.com/mbostock/topojson](https://github.com/mbostock/topojson)
- [https://www.jasondavies.com/maps/rotate/](https://www.jasondavies.com/maps/rotate/)
- [https://codeasart.com/globe/](https://codeasart.com/globe/)
